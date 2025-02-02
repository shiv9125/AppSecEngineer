# Async API Fetcher for AWS Lambda

This repository contains a Python function designed to concurrently fetch data from multiple API endpoints using asynchronous programming with `asyncio` and `aiohttp`. The function is deployable as an AWS Lambda function, ensuring scalability and efficiency.

## Features

- **Asynchronous API Calls**: Leverages `asyncio` and `aiohttp` for concurrent requests.
- **Error Handling**: Handles common errors like client errors and timeouts gracefully.
- **Timeout Mechanisms**: Ensures individual API calls do not hang indefinitely.
- **AWS Lambda Compatible**: Designed to be deployed as an AWS Lambda function with minimal configuration.

## Files

- `async_api_fetch_lambda.py`: Contains the main Lambda function implementation.
- `README.md`: Documentation for the project.

## Installation

1. **Clone the repository**:
   ```bash
   git clone <repository_url>
   cd <repository_name>
   ```

2. **Install dependencies**:
   Ensure you have `aiohttp` installed:
   ```bash
   pip install aiohttp
   ```

3. **Test Locally**:
   You can run the function locally by providing a mock `event` payload:
   ```python
   from async_api_fetch_lambda import lambda_handler

   event = {
       "urls": [
           "https://jsonplaceholder.typicode.com/posts/1",
           "https://jsonplaceholder.typicode.com/posts/2"
       ]
   }
   print(lambda_handler(event, None))
   ```

## Usage

### Lambda Deployment

1. **Package the Function**:
   Create a deployment package with the dependencies:
   ```bash
   pip install -r requirements.txt -t .
   zip -r async_api_fetch_lambda.zip .
   ```

2. **Deploy to AWS**:
   - Go to the AWS Lambda Console.
   - Create a new function or update an existing one.
   - Upload the `async_api_fetch_lambda.zip` file.

3. **Test the Function**:
   Provide an event payload with the `urls` key:
   ```json
   {
       "urls": [
           "https://jsonplaceholder.typicode.com/posts/1",
           "https://jsonplaceholder.typicode.com/posts/2"
       ]
   }
   ```

### Event Payload Format

The Lambda function expects an event payload with the following structure:
```json
{
    "urls": [
        "https://example.com/api/endpoint1",
        "https://example.com/api/endpoint2"
    ]
}
```

### Response Format

The function returns a JSON response with the fetched data or error messages:
```json
{
    "statusCode": 200,
    "body": [
        {
            "id": 1,
            "title": "Example Post 1"
        },
        {
            "error": "Request timed out"
        }
    ]
}
```

## Considerations

- **Rate Limits**: Ensure the target APIs can handle the frequency of your requests.
- **Timeouts**: Adjust the timeout value as necessary for APIs with slower response times.
- **Retries**: Extend the logic to include retries for transient errors.

## Dependencies

- Python 3.7+
- `aiohttp`

## License

This project is licensed under the MIT License. See the LICENSE file for details.

## Acknowledgments

- [aiohttp Documentation](https://docs.aiohttp.org/)
- [AWS Lambda Documentation](https://docs.aws.amazon.com/lambda/index.html)

