# Integration of S3 as storage

Goobi workflow allows operation with S3-compatible storage. It should be noted that a local file system is still required to store the metadata. This means that the files `meta.xml`, `meta_anchor.xml` and their backups, which exist for each process, will continue to be stored in the file system. Only all other data, such as images and OCR results, are stored on the S3 storage area.

To run Goobi with S3 as storage, the following two settings must be set within the configuration file `goobi_config.properties`:

```ini
# global config if s3 should be used
useS3=true

# the bucket that is used for the content that would normally live in /opt/digiverso/goobi/metadata/
S3bucket=workflow-data
```

Goobi workflow uses the AWS Java SDK internally. This means that the credentials for accessing the storage system are read either from `$HOME/.aws` or from environment variables. If another S3 provider is to be used instead of AWS, the connection can be configured relatively granularly. This requires a few more settings within the same configuration files:

```ini
S3AccessKeyID=keyID
S3SecretAccessKey=secretkey
S3Endpoint=http://s3.mygoobi.tld
```

Using S3 as a storage system should basically work with all S3-compatible APIs. During the development of the S3 functionality, both Amazon S3 and [MinIO](https://min.io/) were used for the implementation.