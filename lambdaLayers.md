### Building Lambda Layers Made Easy with SAM Tools

Lambda Layers allow you to store supplementary data and code separately from your main Lambda function, promoting modularity and reusability. However, building these layers can be challenging due to potential OS mismatches and dependencies that may not be suitable for Lambda.

To simplify the process, it is recommended to use AWS Serverless Application Model (SAM) tools to build the layers. This guide demonstrates how to easily create a Lambda layer for JWT verification using Python 3.12, which requires dependencies such as `requests`, `pyjwt`, and `cryptography`.

#### Prerequisites
- Ensure Docker is installed on your machine.

#### Steps to Build a Lambda Layer

1. **Create Directory Structure**:
   Create the necessary directory structure for the Lambda layer.

   ```bash
   mkdir -p python/lib/python3.12/site-packages
   ```

2. **Create `requirements.txt`**:
   List the required dependencies in a `requirements.txt` file.

   ```bash
   echo 'requests\npyjwt\ncryptography' > requirements.txt
   ```

3. **Build the Layer Using Docker**:
   Use a Docker container to install the dependencies in the specified directory.

   ```bash
   docker run -v "$PWD":/var/task "public.ecr.aws/sam/build-python3.12:latest" /bin/sh -c "pip install -r requirements.txt -t python/lib/python3.12/site-packages/; exit"
   ```

4. **Package the Layer**:
   Zip the contents to create the Lambda layer package.

   ```bash
   zip -r lambda_function.zip .
   ```

By following these steps, you can efficiently build Lambda layers with the necessary dependencies, ensuring compatibility and smooth integration with your Lambda functions.
