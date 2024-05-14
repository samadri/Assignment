import logging

# Define logger for API 1
api1_logger = logging.getLogger('api1')
api1_logger.setLevel(logging.INFO)

# Configure log handler for API 1
api1_handler = logging.FileHandler('log1.log')
api1_handler.setFormatter(logging.Formatter('%(asctime)s - %(levelname)s - %(message)s'))
api1_logger.addHandler(api1_handler)

# Example usage in API 1
def some_function():
    try:
        # Code logic
        api1_logger.info('Inside API 1 function')
    except Exception as e:
        api1_logger.error(f'Error in API 1: {str(e)}')
import json
import re

# Simulate command-line arguments with interactive input
args = {}
args['level'] = input('Enter log level (info, error, success) or leave blank: ').strip()
args['message'] = input('Enter search term in log message or leave blank: ').strip()
args['timestamp'] = input('Enter timestamp (YYYY-MM-DDTHH:MM:SSZ) or leave blank: ').strip()
args['source'] = input('Enter log source or leave blank: ').strip()

# Read logs and filter based on user input
with open('log1.log', 'r') as file:
    for line in file:
        log_data = json.loads(line)
        if (not args['level'] or log_data['level'] == args['level']) and \
           (not args['message'] or re.search(args['message'], log_data['log_string'])) and \
           (not args['timestamp'] or log_data['timestamp'] == args['timestamp']) and \
           (not args['source'] or log_data['metadata']['source'] == args['source']):
            print(log_data)
