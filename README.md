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

## Troubleshooting

You might encounter the following error when using elasticsearch:

```bash
ApiError: ApiError(429, 'circuit_breaking_exception', '[parent] Data too large, data for [<http_request>] would be [566122900/539.8mb], which is larger than the limit of [510027366/486.3mb], real usage: [369611440/352.4mb], new bytes reserved: [196511460/187.4mb], usages [model_inference=0/0b, inflight_requests=196511460/187.4mb, request=0/0b, fielddata=0/0b, eql_sequence=0/0b]')
```

This can be fixed by increasing the memory limit for Elasticsearch. To do this, edit line 10 in the `docker-compose.yml` file:

```yaml
environment:
  - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
```

Change the values of `-Xms512m` and `-Xmx512m` for example to `-Xms1g` and `-Xmx1g`.
