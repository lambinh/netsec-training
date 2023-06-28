# Fast IP Lookups for Open Ports and Vulnerabilities

The InternetDB API provides a fast way to see the open ports for an IP address. It gives a quick, at-a-glance view of the type of device that is running behind an IP address to help you make decisions based on the open ports.

The vulnerability information is based on the metadata of a service

1.  The script retrieves data from the Shodan API for a list of IP addresses provided in a text file.
2.  For each IP address, it sends a GET request to the Shodan API and retrieves the corresponding JSON data using the `get_host_data` function.
3.  The JSON data is converted into a table format using the `save_to_table` function.
4.  The script processes each unique IP address, collects the table data, and creates a list of results containing dictionaries.
5.  The script writes the results to two separate output files: `output.json` and `output.csv`.
    -   `output.json` contains the results in a formatted JSON structure, where each IP address is represented as a dictionary.
    -   `output.csv` presents the results as a table with columns, where each row corresponds to an IP address and its associated data.

To use the script:

1.  Prepare a text file containing a list of IP addresses, with one IP address per line.
2.  Ensure that you have the necessary dependencies installed (requests, json, and csv).
3.  Run the script in the command line, providing the text file as a command-line argument:

      python shodan_internetDB.py ip_addresses.txt

4.   The script will retrieve JSON data for each IP address from the Shodan API, convert it into a table format, and store the results in `output.json` and `output.csv`.
5.  Review the generated `output.json` and `output.csv` files to access the retrieved data for each IP address.

You can customize the output file names (`output_file_json` and `output_file_csv`) as per your preference.

Make sure you have the necessary dependencies installed, such as `requests` and `csv`, by running `pip install requests` and `pip install csv` if they are not already installed.

Remember to replace `'output.json'` or `'output.csv'` with your desired output file name if needed.