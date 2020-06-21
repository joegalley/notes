# terraform-errors

#### Error description:
```Error: 
Error importing AWS S3 bucket policy: AuthorizationHeaderMalformed: The authorization header is malformed; the region 'us-east-1' is wrong; expecting 'eu-west-1'
        status code: 400, request id: 9550F897F24D34F2, host id: 8h+QcNWbfppRuRjjWW5JvQTz65hwxUf7zvKLEnQwT1CDZsl2ekCtPs0qxKrjb1AK9h7P1qQHnHk=
```
When running:
```terraform import aws_s3_bucket.my-bucket my-bucket```

#### Explaination:
The message here is pretty cryptic, but it means that there is already a bucket named "my-bucket" in region "eu-west-1". Since S3 buckets must be globally unique, Terraform is assuming that you're trying to 
import "my-bucket" (since that's what you specified in the command), but you are probably not using the region of "eu-west-1" in your Terraform AWS provider. So the message is saying it's in the wrong region. 

#### Fix:
You're probably using the wrong bucket name. Make sure you're using the name of bucket that you actually
own and you specify the correct region (where that bucket lives) in your command.
