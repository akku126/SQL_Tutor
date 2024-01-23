# SQL_Tutor
Download the scipt "Akanksha_Thesis_content_install.sh"

#Copy the script to Engine Container
docker cp '/path/to/script' container_id:/

#Run the script inside engine container
bash Akanksha_Thesis_content_install.sh

##Execute following command inside rdb container terminal
#Get MYSQL terminal
mysql
#add new attribute to 'problem' table
ALTER TABLE its.problem
ADD COLUMN schema_id INT;

#create new table to store schema
CREATE TABLE `its`.`xdata_schema` (
  `id` INT AUTO_INCREMENT PRIMARY KEY,
  `name` VARCHAR(255),
  `schema_file` BLOB,
  'sample_data' BLOB,
  'description' VARCHAR(255)
);

#make schema_id in problem table as foreign key

ALTER TABLE its.problem
ADD CONSTRAINT 'FOREIGN'
FOREIGN KEY ('schema_id')
REFERENCES 'xdata_schema' ('id')
ON DELETE CASCADE
ON UPDATE CASCADE;


##Execute following commands to NOSQL container terminal

#Get mongodb terminal
mongo

#Get inside its 
use its;

#Insert configuration for sql

db.environments.insertOne({"name" : "sql", "editor_mode" : "sql", "compile" : true, "output_format" : "text", "source_ext" : "sql", "binary_ext" : "out", "cmd_compile" : "/var/www/app/compilers/wrappers/xdata_wrapper.sh %s.sql", "cmd_execute" : "%s", "display" : "text", "link_template" : "", "default" : false });

#check whether insertion done for sql

db.environments.find();

#Unable to connect to postgresql?

When running the program,it might happen that the postgresql database server refuses the connection,in this case we might need to edit the "pg_hba.conf" file. Edit the authentication method of
"postgres" user  from 'peer' to 'trust'.Restart postgresql using "service postgresql restart".Re run the installation script so that it can now connect to database server and create roles.

After following above steps, SQL facilities will be accessible from prutor interface.

<b>All other related scripts can be found here: </b><a href="https://github.com/akku126/Mtech_thesis_scripts">https://github.com/akku126/Mtech_thesis_scripts</a>
