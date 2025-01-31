# Elasticsearch installation guide for DSP

This guide is designed for the Data Science in Production course to install Elasticsearch with the LTR plugin and Kibana on your local machine.

## Installation

### Prerequisites

- Docker

### Elasticsearch

1. Clone this repository
2. Run the following command in the root directory of the repository:

```bash
docker compose up
```

3. Open your browser and navigate to `https://localhost:9200` to check if Elasticsearch is running. The default username is "elastic" and the password "mysecurepassword"
4. Copy the elasticsearch certificate to your local machine:

```bash
docker cp elasticsearch:/usr/share/elasticsearch/config/certs/http_ca.crt <path_to_save_certificate>
```

### Kibana

1. Open your browser and navigate to `http://localhost:5601` to check if Kibana is running. You should see a window asking for an enrollment token.
2. Run the following command to get the enrollment token and paste it into the Kibana window:

```bash
docker exec -it elasticsearch bin/elasticsearch-create-enrollment-token -s kibana
```

3. You should now be able to access Kibana.
