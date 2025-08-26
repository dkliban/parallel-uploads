# upload-files

A simple command-line tool for uploading directories to Amazon S3 in parallel.  
It works like a drop-in replacement for:


```bash
aws s3 cp <source_dir> <s3://bucket/prefix> --recursive --only-show-errors
```

…but with configurable concurrency for faster uploads.

## Installation

Clone the repository and install the script as an executable:


```bash
git clone https://github.com/dkliban/parallel-uploads.git
cd upload-files
chmod +x upload-files
```

Optionally move it into your $PATH so it can be used anywhere:

```bash
mv upload-files ~/bin/          # if ~/bin is in your PATH
# or
sudo mv upload-files /usr/local/bin/
```

Make sure you have AWS credentials set up (via aws configure or ~/.aws/config or
environment variables). 

## Usage

```bash
upload-files <source_dir> <s3://bucket/prefix> [concurrency]
```

### Examples

Upload a directory with default concurrency (10):

```bash
upload-files upload s3://my-bucket/workspaces/123/repos/AutoSD
```

Upload with 20 concurrent uploads:

```bash
upload-files upload s3://my-bucket/workspaces/123/repos/AutoSD 20
```

## Notes

Only errors are printed (similar to --only-show-errors).

boto3 automatically uses your AWS credentials and region from ~/.aws/config.

Large files are uploaded with S3 multipart upload for efficiency.
