
<html lang="en">
<head>
    <meta charset="UTF-8">
    <style>
    h1 {
        font-size: 36px;
        margin-bottom: 40px;
        text-align: center;
    }
    .logos {
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .logos img {
        margin: 0 20px;
        height: 100px;
    }
    .badges {
        font-family: Arial, sans-serif;
        padding: 50px;
        text-align: center;
        margin-top: 40px;
    }
    .badges img {
        margin: 0 10px;
    }
    </style>
</head>

<body>
<h1>Real-Time Data Visualization Stack: InfluxDB, Grafana, and Docker Compose</h1>

<div class="logos">
    <img src="https://www.influxdata.com/wp-content/uploads/2021/11/influxdb-logo.png" alt="InfluxDB Logo">
    <img src="https://www.docker.com/wp-content/uploads/2022/03/Moby-logo.png" alt="Docker Logo">
    <img src="https://grafana.com/static/img/grafana_logo.svg" alt="Grafana Logo">
</div>

<div class="badges">
    <a href="https://github.com/CaptainIgl00/grafana-influxdb-docker-compose/actions">
        <img src="https://github.com/CaptainIgl00/grafana-influxdb-docker-compose/workflows/Build/badge.svg" alt="Build Status">
    </a>
    <a href="https://github.com/CaptainIgl00/grafana-influxdb-docker-compose/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License">
    </a>
    <a href="https://github.com/CaptainIgl00/grafana-influxdb-docker-compose/releases">
        <img src="https://img.shields.io/github/v/release/CaptainIgl00/grafana-influxdb-docker-compose" alt="Latest Release">
    </a>
</div>
</body>
</html>

## Description

This project sets up a complete **monitoring environment** using **Docker Compose** to orchestrate **InfluxDB** and **Grafana**. It allows for **collecting**, **storing**, and **visualizing real-time metric data**. The configuration includes automatic initialization of InfluxDB and automatic configuration of Grafana with pre-configured data sources and dashboards.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## Prerequisites

- Docker installed on your machine.
- Docker Compose installed (version 3.7 or higher recommended).

## Installation

1. Clone the Repository

```bash
git clone https://github.com/CaptainIgl00/grafana-influxdb-docker-compose.git
cd grafana-influxdb-docker-compose
```

2. Modify the .env file with your own information

```env
INFLUXDB_DATABASE=db
INFLUXDB_USERNAME=user
INFLUXDB_ORG=org
INFLUXDB_PASSWORD=userpassword
INFLUXDB_TOKEN='token'

GRAFANA_USERNAME=admin
GRAFANA_PASSWORD=adminpassword
```
**Note**: Make sure to replace the values with your own information. Avoid using special characters such as quotes in the passwords to prevent interpretation issues.

3. Run the Docker Compose file

```bash
docker-compose up -d
```

4. Access Grafana at http://localhost:3000 and InfluxDB at http://localhost:8086

## Usage

In order to add **custom dashboards**, you can use the Grafana interface.

1. Create or Export a Dashboard
    - Create a new dashboard in Grafana.
    - Export it as JSON via Share > Export > Save to file.

2. Add the Dashboard to the Project

    - Place the exported JSON file into the grafana-dashboards/ folder.

3. Next time you start the project, the dashboard will be automatically added to Grafana.

## Project Structure

```
grafana-influxdb-docker-compose/
├── docker-compose.yml           # Docker Compose file
├── .env                         # InfluxDB and Grafana credentials
├── grafana-dashboards/          # Folder for custom dashboards
│    └── Example Dashboard.json  # Example dashboard
│
├── grafana-provisioning/        # Folder for Grafana provisioning
    ├── datasources/
    │   └── datasource.yml       # Configures InfluxDB as the default data source
    │
    └── dashboards/
        └── dashboard.yml        # Automatically loads dashboards from grafana-dashboards/
```

## Troubleshooting

### Connection Issues with InfluxDB

- Verify that the environment variables are correctly defined in the .env file.

- Ensure that the init-influxdb service ran successfully by checking the logs:

```bash
docker-compose up
```

### Dashboards or Data Sources Not Loaded

- Check that the provisioning files are correctly placed in grafana-provisioning/datasources/ and grafana-provisioning/dashboards/.

- Review Grafana logs for any errors:

```bash
docker-compose logs -f grafana-influxdb-docker-compose-grafana-1
```

- Make sure that the InfluxDB token doesn't contain special characters that could be badly interpreted.

### Environment Variables Not Expanded in YAML Files

- Ensure that variables are referenced using the `${VARIABLE}` syntax in the provisioning YAML files.

- The environment variables must be exported within the Grafana container. You can verify them with:

```bash
docker exec -it grafana-influxdb-docker-compose-grafana-1 env | grep GF_
```

## Contributing

Contributions are welcome! If you find bugs or have suggestions for improvement, feel free to open an issue or a pull request.

## License

This project is licensed under the GPL-3.0 License. See the [LICENSE](LICENSE) file for details.
