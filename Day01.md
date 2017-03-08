##For some reason I was interested in which employee sold the most Tofu ad thus generated the most tofu based income...
'''sql  
SELECT orderdetails.quantity, products.productname, products.price, employees.firstname  
FROM orderdetails  
JOIN products  
ON orderdetails.productID=products.productID  
JOIN categories  
ON products.categoryid=categories.categoryID  
JOIN orders  
ON orders.orderID=orderdetails.orderID  
JOIN employees  
ON employees.employeeID=orders.employeeID  
WHERE productname LIKE '%Tofu%'  
ORDER BY quantity DESC;  
'''  

##Two tables containing mutiple columns for both the samples and the mutations. 
'''sql  
CREATE TABLE Mutations  
(  
MutationID int,
ChrNumber int,  
ChrPosition int,  
MutationType varchar(255),  
Genotype varchar(3),  
NucleotideMutation varchar(3),  
GeneLocation varchar(255),  
Protein varchar(255)  
);  

CREATE TABLE Samples  
(  
sampleID int,  
Age int,  
Gender varchar(6),  
Disease varchar(255),  
AssociatedGenes varchar(255),
PRIMARY KEY (SampleID)
FOREIGN KEY (MutationID) REFERENCES Samples(SampleID)
);  
'''  
