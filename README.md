
# ssb-search

**ssb-search** is a command-line application for querying logs stored in an SSB logging appliance through its API. This tool is designed to quickly search and retrieve log data directly from the command line.

## Features

- **Log searching**: Query logs using the filters that SSB-s search interface provides.
- **Config file support**: Appliance IP/hostname, logspace name, username and password can be set via config file or interactively.
- **Pagination and Limits**: Fetch large log datasets with pagination and configurable result limits, by default retrieved logs are limited to 100


## Requirements

- **Python 3.8 or higher**
- The following Python libraries:
  - `requests`

Install dependencies using `pip`:
```bash
pip install -r requirements.txt
```

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/evetovicsm/ssb-cli-search.git
   cd ssb-cli-search
   ```

2. Install the required packages:
   ```bash
   pip install -r requirements.txt
   ```

3. Make the script executable:
   ```bash
   chmod +x ssb-search
   ```

4. (Optional) Add the application to your `PATH`:
   ```bash
   export PATH=$PATH:$(pwd)
   ```

## Usage

### Basic Command Syntax
```bash
 ./ssb-search [-h] [--ssb_appliance SSB_APPLIANCE] [--logspace LOGSPACE] [--from-timestamp FROM_TIMESTAMP] [--to-timestamp TO_TIMESTAMP] [--offset OFFSET] [--limit LIMIT] search_term
```

### Examples

1. **Simple logs search:**
   ```bash
    ./ssb-search --ssb_appliance ssb1.test.demo --logspace linux-logs ssh
   ```

2. **Filter logs by host:**
   ```bash
   ./ssb-search --ssb_appliance ssb1.test.demo --logspace linux-logs "HOST:www1 ssh"
   ```

4. **Paginated search:**
   ```bash
    ./ssb-search --ssb_appliance ssb1.test.demo --logspace linux-logs "HOST:www1 ssh"
   ```

### Options

| Option               | Description                                                                                       |
|----------------------|---------------------------------------------------------------------------------------------------|
| ` --help `           | Show help and usage information.                                                                  |
| `--ssb_appliance`    | The hostname or ip address of the SSB appliance.                                                  |
| `--logspace`         | The name of the logspace to search in                                                             |
| `--from-timestamp`   | The starting timestamp for search. Default to 0.                                                  |
| `--to-timestamp`     | The ending timestamp for search. Default to 9999999999.                                           |
| `--offset`           | If the number of search result is greater then the set limit. Send result dataset by this offset. |
| `--limit`            | Limit search results, defaults to 100                                                             |

### Positional arguments
  search_term           The search expression to search for.
  
## Configuration

You can use a configuration file to store settings for applaince ip/hostname, the logspace name, and the authetication data. Save a file named `ssb-search.cfg` in your home directory with the following format:
```ini
[DEFAULT]
 SSB_APPLIANCE = ssb1.test.demo
 LOGSPACE_NAME = center
 USERNAME = logspace_reader
 PASSWORD = SecretPassword
```

Run the application without specifying these options to use the defaults:
```bash
./ssb-search "HOST:www1 ssh"
```

## Contributing

Contributions are welcome! Please follow these steps:
1. Fork the repository.
2. Create a new branch for your feature or bug fix.
3. Submit a pull request.

## Licensing

This project is licensed under the MIT License. See the [LICENSE](LICENSE.md) file for details.
