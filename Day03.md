# Advanced-Bioinformatics-Daily-Assignments
For the course advanced bioinformatics

## This is the RDF template (same as the JSON template used for the PIK3CA file)
=HEADER  
@prefix : <http://matthijs2.org/rdf/ns#> .  
=BODY   
<%  
id = ['chr'+rec.chr,rec.pos,rec.ref,rec.alt].join('_')  
%>  
:<%= id %>  
  :query_id "<%= id %>";  
  :chr "<%= rec.chr %>" ;  
  :ref "<%= rec.ref %>" ;  
  :alt "<%= rec.alt.join("") %>" ;  
  :pos <%= rec.pos %> .  

## Creating the RDF file from the PIK3CA.vcf with the RDF template:
cat gene_PIK3CA.vcf | bio-vcf -v --template PIK3CA_template2.erb > PIK3CA.rdf
## Then uploading it to the guix.genenetwork (rapper not working on local machine, so I skipped that part)
rdf=PIK3CA.rdf  
uri=http://guix.genenetwork.org/data/http://matthijs2.org/data/$rdf  
curl -T $rdf -H 'Content-Type: application/x-turtle' $uri  

## Creating a simple python script that queries the PIK3CA RDF data on chromosome and position (in this case chromosome X and any position that is larger than 169000000)
import requests  
import subprocess  
  
host = "http://guix.genenetwork.org/"  
  
query = """  
PREFIX : <http://matthijs2.org/rdf/ns#>  
SELECT * {    
    ?id :chr "X" .  
    ?id :alt ?alt .  
    ?id :pos ?pos .  
    FILTER (?pos > 169000000) .  
}   
"""  
r = requests.post(host + "sparql/", data={ "query": query, "output": "text" })  
if r.status_code != requests.codes.ok:  
    sys.exit(1)  
print r.text  
