In IAM Creating Access Key and Secret Key:
1.	Left Corner Account Name
2.	Security credentials
3.	Scroll down Access Key> create Access key
4.	Select check box I understand creating a root access key is not a best practice, but I still want to create one.
5.	Press on Create Access Key.
6.	Copy Access Key and Secret Key.
Access Key: -----------
Secret Key: -----------

S3 Bucket Creation:
1.	Go to link: https://s3.console.aws.amazon.com/s3/home?region=us-east-1
2.	Create Bucket
3.	Choose AWS Region (S3 Buckets are Region Specific)
4.	Enter Bucket Name 
5.	Object Ownership, select ACLs enabled
6.	Uncheck Block all public access
7.	Select checkbox I acknowledge that the current settings might result in this bucket and the objects within becoming public.
8.	Create Bucket
9.	Click on Bucket Name, go to permissions tab
10.	Scroll down last, see Cross-origin resource sharing (CORS)> edit.
11.	Paste

[
    {
        "AllowedHeaders": [
            "*"
        ],
        "AllowedMethods": [
            "GET",
            "POST",
            "PUT"
        ],
        "AllowedOrigins": [
            "*"
        ],
        "ExposeHeaders": []
    }
]

#Server port
server.port=9090

#Database Properties
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://proje.cvmak7.us-east-1.rds.amazonaws.com:3306/iuy
spring.datasource.username=root
spring.datasource.password=rqw1er44

#JPA Configuration Properties:
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect

#AWS S3 properties
spring.s3.access.key=AKI6677QY3KENVL8uut
spring.s3.secret.key=P7nuNLBLM9EUkdlhlKVlfXfX0u1
spring.s3.bucket.name=fileupyyeheb23jjk

@Configuration
@Getter
public class S3Configuration {
	@Value("${spring.s3.access.key}")
	private String accessKey;
	@Value("${spring.s3.secret.key}")
	private String secreteKey;
	@Value("${spring.s3.bucket.name}")
	private String bucketName;
	@Bean
	public BasicAWSCredentials getCredentials() {
		return new BasicAWSCredentials(accessKey,secreteKey);
	}
	@Bean
	public AmazonS3 getClient() {
		return AmazonS3ClientBuilder
	                 .standard()
		        .withCredentials(new AWSStaticCredentialsProvider(this.getCredentials()))
                          .withRegion(Regions.US_EAST_1)
                          .build();
	}
}



