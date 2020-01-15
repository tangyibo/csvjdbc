# csvjdbc
访问文本文件的JDBC驱动

# Usage

The CsvJdbc driver is used just like any other JDBC driver:

- download csvjdbc.jar and add it to the Java CLASSPATH or use pom.xml config flowing:
```
		<dependency>
			<groupId>net.sourceforge.csvjdbc</groupId>
			<artifactId>csvjdbc</artifactId>
			<version>1.0.35</version>
		</dependency>
```
- load the driver class, (its full name is org.relique.jdbc.csv.CsvDriver)
- use DriverManager to connect to the database (the directory or ZIP file)
- create a statement object
- use the statement object to execute an SQL SELECT query
- the result of the query is a ResultSet

# Example

```
	public static void main(String[] args) throws ClassNotFoundException, SQLException {
	    // Load the driver.
	    Class.forName("org.relique.jdbc.csv.CsvDriver");

	    // Create a connection to directory given as first command line
	    // parameter. Driver properties are passed in URL format
	    // (or alternatively in a java.utils.Properties object).
	    //
	    // A single connection is thread-safe for use by several threads.
	    String url = "jdbc:relique:csv:D:\\?separator=,&fileExtension=.csv";
	    Connection conn = DriverManager.getConnection(url);

	    // Create a Statement object to execute the query with.
	    // A Statement is not thread-safe.
	    Statement stmt = conn.createStatement();

		// Select the ID and NAME columns from sample.csv
		ResultSet results = stmt.executeQuery("SELECT ID,NAME FROM sample");
		ResultSetMetaData meta = results.getMetaData();
		while (results.next()) {
			for (int i = 0; i < meta.getColumnCount(); i++) {
				System.out.print(meta.getColumnName(i + 1) + "=" + results.getString(i + 1) + ";");
			}
			System.out.println();
		}
		conn.close();

		// Clean up
		conn.close();
	}
```
