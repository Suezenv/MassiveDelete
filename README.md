# MassiveDelete
A simple Alfresco massive deletion batch.

The program aims to overcome Alfresco API limits for deleting a large set of nodes in your repository in a simple way. Before you have to prepare the set of nodes to delete by sending a simple SQL query to Alfresco.

SELECT nodes.UUID FROM alf_node nodes, alf_qname names WHERE nodes.type_qname_id=names.id AND names.local_name='PUT_YOUR_TYPE_HERE';
	
# How to build it yourself
Clone the project and configure the batch by editing the `conf.properties` file. Then run `mvn clean package`.

You can provide an external 'conf.properties' file; the configuration file needs to have the following entries:

`alfresco.url=http://localhost:8080/alfresco`

`alfresco.user=admin`

`alfresco.password=alfresco`


To execute the program you can use i.e:

	JAVA_FLAGS=-Dhttp.proxyHost=10.0.0.100 -Dhttp.proxyPort=8800
	java ${JAVA_FLAGS}

	cd target; java -jar MassiveDelete-1.0-jar-with-dependencies.jar path_to_UUID_LIST_file

	-- using built-in configuration file
	nohup /opt/alfresco/java/bin/java -cp  "MassiveDelete-1.0.jar:$(find lib/ -name "*.jar" | sed -e 's,^,:,g' | tr -d '\n')" MassiveDelete path_to_UUID_LIST_file &

	-- using an external configuration file
	nohup /opt/alfresco/java/bin/java -Dconf=path_to_conf_file -cp  "MassiveDelete-1.0.jar:$(find lib/ -name "*.jar" | sed -e 's,^,:,g' | tr -d '\n')" MassiveDelete path_to_UUID_LIST_file &	


# Author
Christian Tiralosi

Francesco Fornasari
