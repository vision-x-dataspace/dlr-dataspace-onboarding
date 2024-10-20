# 2. Set up Storage

## Install minio client

To install the MinIO client (`mc`) on a Linux system, follow these steps:

### 1. Download MinIO Client (mc)

You can download the latest version of `mc` using `wget`:

```bash
wget https://dl.min.io/client/mc/release/linux-amd64/mc
```

### 2. Make the Binary Executable

After downloading, you need to give the `mc` binary executable permissions:

```bash
chmod +x mc
```

### 3. Move the Binary to a System-Wide Location

Move the `mc` binary to a directory in your system's PATH (such as `/usr/local/bin`):

```bash
sudo mv mc /usr/local/bin/
```

### 4. Verify the Installation

To ensure that `mc` is installed correctly, you can check the version:

```bash
mc --version
```

## Set up the storage for the provider

### 1. Set an alias for the provider endpoint

`mc alias set provider-minio http://minio-alice.83a9eabf.nip.io/ aliceawsclient aliceawssecret`

### 2. Make a bucket for the provider

`mc mb "provider-minio/<provider_bucket_name>`

Please replace `<provider_bucket_name>` with a **unique** name.

### 3. Upload a file to the provider bucket

`touch test-file.txt`

`mc cp test-file.txt provider-minio/<provider-bucket-name>`

Please replace `<provider_bucket_name>` with the name of the provider bucket you just created.

## Set up the storage for the consumer

### 1. Set an alias for the consumer endpoint

`mc alias set consumer-minio http://minio-bob.83a9eabf.nip.io/ bobawsclient bobawssecret`

### 2. Make a bucket for the consumer

`mc mb "consumer-minio/<consumer_bucket_name>`

Please replace `<consumer_bucket_name>` with a **unique** name.
