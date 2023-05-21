# Installing JDK 17, PostgreSQL, pgAdmin, SonarQube, and SonarScanner

This guide provides step-by-step instructions for installing JDK 17, PostgreSQL, pgAdmin, SonarQube, and SonarScanner.

## Table of Contents
- [Installing JDK 17](#installing-jdk-17)
- [Installing PostgreSQL and pgAdmin](#installing-postgresql-and-pgadmin)
- [Creating User and Database in PostgreSQL](#creating-user-and-database-in-postgresql)
- [Installing SonarQube and SonarScanner](#installing-sonarqube-and-sonarscanner)
- [Configuring SonarQube](#configuring-sonarqube)
- [Launching SonarQube and Logging In](#launching-sonarqube-and-logging-in)
- [Creating a New Project in SonarQube](#creating-a-new-project-in-sonarqube)
- [Analyzing a Project with SonarScanner](#analyzing-a-project-with-sonarscanner)

## Installing JDK 17

1. Visit the official Oracle website or your preferred JDK distribution provider to download JDK 17 for your operating system.

2. You can find JDK 17 at [Oracle JDK Downloads](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html).

3. Follow the installation instructions provided by the JDK distribution for your specific operating system.

4. Verify the JDK installation by opening a terminal or command prompt and running 
 
  ```bash
    java -version
  ```
 You should see the JDK version information displayed.

## Installing PostgreSQL and pgAdmin

1. Download the PostgreSQL installer for your operating system from the official PostgreSQL website.

2. You can find PostgreSQL downloads at [PostgreSQL Downloads](https://www.postgresql.org/download/).

3.  Run the installer and follow the installation wizard, selecting the desired installation options.

4.  During the installation, set a password for the PostgreSQL superuser (postgres).

5.  Remember this password as you will need it later.

6.  Download pgAdmin, the graphical administration tool for PostgreSQL, from the official pgAdmin website.

7.  You can find pgAdmin downloads at [pgAdmin Downloads](https://www.pgadmin.org/download/).

8.  Install pgAdmin by running the downloaded installer and following the installation instructions.

9.  Launch pgAdmin and create a new server connection by right-clicking on "Servers" in the left sidebar and selecting `Create > Server...`.

10. In the "Connection" tab, provide the following details:
    - `Host`: localhost
    - `Port`: 5432
    - `Maintenance` database: postgres
    - `Username`: postgres
    - `Password`: [enter the password you set during installation]

## Creating User and Database in PostgreSQL

1. Open pgAdmin and connect to the PostgreSQL server you created in the previous step.

2. Right-click on "Login/Group Roles" and select `Create > Login/Group Role...`.

3. Enter "sonar" as the `Name` and set the `Password` to "sonar". Leave the other fields as default.

4. Switch to the `Privileges` tab and check the Can login? option.

5. Click `Save` to create the user.

6. Right-click on "Databases" and select `Create > Database...`.

7. Enter "sonarqube" as the `Name` and select "sonar" as the `Owner`.

8. Click `Save` to create the database.

## Installing SonarQube and SonarScanner

1. Download the SonarQube distribution from the official SonarQube website at [SonarQube Downloads](https://www.sonarqube.org/downloads/). Extract the downloaded archive to a directory of your choice.

2. Extract the downloaded archive to a directory of your choice.

3. Open a terminal or command prompt and navigate to the directory where SonarQube was extracted.

4. Start SonarQube by running the appropriate command based on your operating system:
    - On Linux/macOS: `./bin/[OS]/sonar.sh start`
    - On Windows: `.\bin\[OS]\StartSonar.bat`

      Replace `[OS]` with the appropriate directory name for your operating system (e.g., linux-x86-64, windows-x86-64).

5. Once SonarQube has started, access the SonarQube web interface by opening your web browser and navigating to [http://localhost:9000](http://localhost:9000).

6. Download SonarScanner from the official SonarQube website at [SonarScanner Downloads](https://docs.sonarqube.org/latest/analysis/scan/sonarscanner/).

7. Extract the downloaded archive to a directory of your choice.

8. Configure SonarScanner by opening the `sonar-scanner.properties` file located in the `conf` directory.

9. Update the following properties in the `sonar-scanner.properties` file:

    ```less
    sonar.host.url=http://localhost:9000
    sonar.login=[SONARQUBE_TOKEN]
    ```
    Replace `[SONARQUBE_TOKEN]` with the token generated in the SonarQube web interface (Administration > Security > Tokens).

10. Save the changes and close the file.
## Configuring SonarQube

1. In the SonarQube web interface, log in with the default administrator credentials (admin/admin).

2. Navigate to `Administration > Configuration > General Settings`.

3. Scroll down to the `Database` section and configure the following properties:

    - JDBC URL: jdbc:postgresql://localhost/sonarqube?currentSchema=public
    - JDBC Username: sonar
    - JDBC Password: sonar

4. Click `Save` to apply the changes.

## Launching SonarQube and Logging In

1. Open a terminal or command prompt and navigate to the directory where SonarQube was extracted.

2. Start SonarQube by running the appropriate command based on your operating system:

    - On Linux/macOS: `./bin/[OS]/sonar.sh start`
    - On Windows: `.\bin\[OS]\StartSonar.bat`
     Replace `[OS]` with the appropriate directory name for your operating system (e.g., linux-x86-64, windows-x86-64).

3. Once SonarQube has started, access the SonarQube web interface by opening your web browser and navigating to http://localhost:9000.

4. Log in using the default administrator credentials:

   - `Username`: admin
   - `Password`: admin

## Creating a New Project in SonarQube

1. In the SonarQube web interface, click on the "+" icon in the top-right corner to create a new project.

2. Provide a project key, name, and optional description for the project.

3. Click `Create` to create the project.

## Analyzing a Project with SonarScanner

1. Download any public project from GitHub or another source and extract it to a local directory.

2. Open a terminal or command prompt and navigate to the project's root directory.

3. Run the following command to analyze the project with SonarScanner:

     ```
        sonar-scanner
     ```
4. SonarScanner will analyze the code and send the results to SonarQube.

5. Once the analysis is complete, you can view the code quality metrics and analysis reports in the SonarQube web interface.

Make sure to consult the official documentation for each tool to find the latest versions of the dependencies and for more detailed instructions and troubleshooting tips if you encounter any issues during the installation or configuration process.installation or configuration process.
