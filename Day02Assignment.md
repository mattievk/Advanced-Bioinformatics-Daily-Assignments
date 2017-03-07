# Advanced-Bioinformatics-Daily-Assignments
For the course advanced bioinformatics

##Assignment Day02 (replacement)
'''unix
wget https://github.com/pjotrp/bioruby-vcf/raw/master/test/data/input/gatk_exome.vcf

vi gatk_template.json:
	{
	"rec":{
			"chr": "<%= rec.chrom %>",
            "pos": <%= rec.pos %>,
            "ref": "<%= rec.ref %>",
            "alt": "<%= rec.alt[0] %>",
            "dp":  <%= rec.info.dp %>
			}
	}

cat gatk_exome.vcf |bio-vcf --template gatk_template.json > gatk_exome.json

mongoimport --db gatk --collection vcf --drop --file gatk_exome.json --jsonArray

mongo

use gatk

X = lower limit position
Y = upper limit position

db.vcf.find( { "red.pos": { $gt: X , $lt: Y }} ).count()
'''
