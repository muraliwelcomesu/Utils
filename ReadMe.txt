1. Lov_Modification.py:
   Requirement: Lov Queries needs to be changed in multiple RAD Files.[Table Name X to be Changed to Another Table Y].
	            Same Change is required across all Files.
				
			  Path 		    : List containing the local path for RAD files.
			  l_search_list : Name of Tables that needs to be searched in the RAD which requires modification.
			  Processing Logic:  
								1) Function prepare_excel to be called first which searches the RAD Xmls in the folders mentioned in the path
								   for the lov queries that contains the table names specified in the search list and writes the RAD File name, 
								   Lov query in an Excel [Output.xlsx] in the working directory.
								2) Once the lov queries are identified this can be manually modified as per the requirement.
								3) After modification, update_xml function to be called for updating the RAD xml after which bulk generation can be done.
			 Python Libraries Used:
								xml.etree ElementTree => Xml operations.
								openpyxl => Excel Operations.
								os - System Operations
--*************************************************************************************************************************************************************
2. Search_UM.py
	Search for a particular text in User manuals.
	Base usermanual url to be provided in url variable.
	Default version is 14.2 for which url is already defined.If searching for other versions, pls provide the url.
	l_search_Str => Search string.
	Starting from the base url,the string is searched and if found stored in the search list and all other links in the page is searched recursively.
	Finally the serached results and log file which contains the list of pages searched will be written as a file in predefined folder.
	Search results will be available in <search_string>_Results.txt and Log file will be available in <search_string>_log.txt.
	
	Python Libraries Used: Beautiful Soup for Webscraping
--*********************************************************************************************************************************************************
3. Export_Tables.py
   Export specific tables from one schema to another schema. New tables can be of different name from original tables.
   Specific rows of the tables alone can be exported by providing the condition.
   Input: source schema, destination schema, list of tables to be exported.
   For each tables given,
      fetch_records: Open connection to source schema and query the tables and fetch the results in a python list.
	  insert_records: Check if table already available in destination schema, if not create the same using system tables in schema1.
					  Insert the fetched records from the list to the destination table.
	
	Tech Details:
 1) Convert query result to a list [fetch_records] 
 2) Convert two lists to a dict [get_cols_struct]
 3) Querying a table
 4) Creating a table
 5) Inserting a table (with multiple records from a list of values).
 
	Python Libraries Used:
						cx_Oracle
 --********************************************************************************************************************************************************
  4. List_Files.py
	List of files in server needs to be compiled in the database in the order of creation time after copying the same files to the local system and preparing 
	a script file to compile the same. All these to be automated.
   get_files_modified_time: Get list of files from server to local machine in the order of creation time and prepare a script file for compilation in proper order.
   get_files :Given a path, this funtion to prepare the list of files in its folder and its subfolder for compilation.
   Customising the script file to add additional comments [like prompt message on each lines ].
   Python Libraries Used:
						os and Shutil.
--******************************************************************************************************************************************************
5. Files_Compare.py
   Compare the list of all files between two directories and its sub folders and list out the differences in a file.
   Input: Dir1, Dir2
   Output: File in predefined path with the following details:
		--> Files different in dir1 and dir2
		--> Files available in dir1 but not in dir2
		--> Files available in dir2 but not in dir1
	Python Libraries Used:
			filecmp and os.
--******************************************************************************************************************************************************
6. extract_names.py
    Finds specific text in a file. i,e finding the no.of.tables getting selected/inserted/updated/deleted in a package and to extract the tables that 
	were selected/inserted/updated/deleted.
	Input: Text file [plsql package].
	Search string: 'Select * From' << This can be customised>>
	Output: Text file with the list of tables selected in the package.
--******************************************************************************************************************************************************