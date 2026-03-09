# Practical Guidelines for Installing and Analyzing a Python App using SonarQube

 Step 1: Install SonarQube
 1. Download the SonarQube Community Edition from the official website: https://www.sonarsource.com/
 2. Extract the downloaded archive to your desired location.
 3. Start SonarQube by running the appropriate script for your OS:
    - On Windows: Execute `StartSonar.bat` located in the `bin\windows-x86-64` directory.
    - On Linux: Run `./sonar.sh start` located in the `bin/linux-x86-64` directory.
 4. Open a browser and navigate to `http://localhost:9000` to access the SonarQube dashboard.
 5. Log in using the default credentials (admin/admin) and change the password upon first login.

# Step 2: Install SonarScanner
 1. Download SonarScanner from the official website: https://docs.sonarqube.org/latest/analysis/scan/sonarscanner/
 2. Extract the archive and add the `bin` directory to your system's PATH environment variable.
 3. Verify the installation by running `sonar-scanner -v` in your terminal.

# Step 3: Analyze the Python Application
 1. Navigate to the root directory of your Python project.
 2. Ensure the `sonar-project.properties` file is correctly configured. For example:
```bash
    sonar.projectKey=vulnerable-python-app
    sonar.projectName=Vulnerable Python App
    sonar.sources=.
    sonar.language=py
    sonar.python.version=3
```
 3. Run the SonarScanner command:
    `sonar-scanner -Dsonar.host.url http://localhost:9000 -Dsonar.login=<Sonar-TOKEN>`
 4. Wait for the analysis to complete. Results will be available on the SonarQube dashboard under the specified project key.

# Notes:
 - Ensure that SonarQube is running before executing the `sonar-scanner` command.
 - Install any required Python dependencies for your project before analysis.
 - Refer to the SonarQube documentation for advanced configuration options.