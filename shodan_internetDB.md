# Fast IP Lookups for Open Ports and Vulnerabilities

The Shodan InternetDB API provides a fast way to see the open ports for an IP address. It gives a quick, at-a-glance view of the type of device that is running behind an IP address to help you make decisions based on the open ports.

The vulnerability information is based on the metadata of a service
1.  The script reads a list of IP addresses from a text file provided as a command-line argument.
2.  It retrieves JSON data for each IP address from the Shodan API using the `get_host_data` function.
3.  The JSON data is parsed and converted into a table format using the `save_to_table` function.
4.  The script processes each IP address, collects the table data, and creates a list of results.
5.  The results include the IP address and its associated table data as a dictionary.
6.  The script writes the results to a JSON file or a CSV file, depending on the desired output format.
    -   For JSON output, it uses the `json.dump()` function to write the results to a JSON file.
    -   For CSV output, it uses the `csv.DictWriter` to write the results to a CSV file.

To use the script:

1.  Prepare a text file containing a list of IP addresses, with one IP address per line.
2.  Run the script in the command line, providing the text file as a command-line argument:

      ``` python shodan_internetDB.py ip_addresses.txt ```

1.  The script will retrieve JSON data for each IP address, parse it, and create a table of results.
2.  Depending on the desired output format (JSON or CSV), the script will generate the corresponding output file (`output.json` or `output.csv`) containing the IP addresses and their associated table data.

Make sure you have the necessary dependencies installed, such as `requests` and `csv`, by running `pip install requests` and `pip install csv` if they are not already installed.

Remember to replace `'output.json'` or `'output.csv'` with your desired output file name if needed.
