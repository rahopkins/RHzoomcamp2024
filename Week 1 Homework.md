**Question 1. Knowing docker tags**
  Answser = -rm
  Steps:
    run command docker run --help and look for correct option
   

**Question 2. Understanding docker first run**
  Answer = 0.42.0
  Steps: Run pip list and look for the wheel package


**Question 3. Count records**
Answer = 15612
Query:
select count(*) from green_taxi_data
where
lpep_pickup_datetime between '2019-09-18 00:00:00' and '2019-09-18 23:59:59'
and
lpep_dropoff_datetime between '2019-09-18 00:00:00' and '2019-09-18 23:59:59';


**Question 4. Largest trip for each day**
Answer = 2019-09-26
Query:
select lpep_pickup_datetime, trip_distance from green_taxi_data
order by trip_distance desc;


**Question 5. Three biggest pick up Boroughs**
Answer = Brooklyn, Manhattan, Queens
Query:
select 
	z."Borough", sum(g.total_amount) as sum_total
from green_taxi_data g
join zones z on z."LocationID" = g."PULocationID"
where 
	g.lpep_pickup_datetime between '2019-09-18 00:00:00' and '2019-09-18 23:59:59'
	and
	z."Borough" != 'Unknown'
group by z."Borough"
order by sum_total desc;


**Question 6. Largest tip**
select 
	g.tip_amount, zpu."Zone", zdo."Zone"
from 
	green_taxi_data g,
	zones zpu,
	zones zdo
where
	g."PULocationID" = zpu."LocationID" and
	g."DOLocationID" = zdo."LocationID" and
	zpu."Zone" = 'Astoria'
order by g.tip_amount desc


**Question 7. Creating Resources**
After running terraform apply:

google_bigquery_dataset.rh_dataset: Refreshing state... [id=projects/de-zoomcamp-2024-409204/datasets/demo_dataset]

Terraform used the selected providers to generate the following execution plan. Resource actions are
indicated with the following symbols:
  + create
-/+ destroy and then create replacement

Terraform will perform the following actions:

  # google_bigquery_dataset.rh_dataset must be replaced
-/+ resource "google_bigquery_dataset" "rh_dataset" {
      ~ creation_time                   = 1705724971530 -> (known after apply)
      ~ dataset_id                      = "demo_dataset" -> "rh_dataset" # forces replacement
      + default_collation               = (known after apply)
      - default_partition_expiration_ms = 0 -> null
      - default_table_expiration_ms     = 0 -> null
      ~ effective_labels                = {} -> (known after apply)
      ~ etag                            = "sYT0j2XBnPVR8kyiv7t9BQ==" -> (known after apply)
      ~ id                              = "projects/de-zoomcamp-2024-409204/datasets/demo_dataset" -> (known after apply)
      ~ is_case_insensitive             = false -> (known after apply)
      - labels                          = {} -> null
      ~ last_modified_time              = 1705724971530 -> (known after apply)
      + max_time_travel_hours           = (known after apply)
      ~ self_link                       = "https://bigquery.googleapis.com/bigquery/v2/projects/de-zoomcamp-2024-409204/datasets/demo_dataset" -> (known after apply)
      + storage_billing_model           = (known after apply)
      ~ terraform_labels                = {} -> (known after apply)
        # (3 unchanged attributes hidden)

      - access {
          - role          = "OWNER" -> null
          - user_by_email = "terraform-runner@de-zoomcamp-2024-409204.iam.gserviceaccount.com" -> null
        }
      - access {
          - role          = "OWNER" -> null
          - special_group = "projectOwners" -> null
        }
      - access {
          - role          = "READER" -> null
          - special_group = "projectReaders" -> null
        }
      - access {
          - role          = "WRITER" -> null
          - special_group = "projectWriters" -> null
        }
    }

  # google_storage_bucket.rh-bucket will be created
  + resource "google_storage_bucket" "rh-bucket" {
      + effective_labels            = (known after apply)
      + force_destroy               = true
      + id                          = (known after apply)
      + location                    = "US"
      + name                        = "terraform-rh-terra-bucket"
      + project                     = (known after apply)
      + public_access_prevention    = (known after apply)
      + self_link                   = (known after apply)
      + storage_class               = "STANDARD"
      + terraform_labels            = (known after apply)
      + uniform_bucket_level_access = (known after apply)
      + url                         = (known after apply)

      + lifecycle_rule {
          + action {
              + type = "AbortIncompleteMultipartUpload"
            }
          + condition {
              + age                   = 1
              + matches_prefix        = []
              + matches_storage_class = []
              + matches_suffix        = []
              + with_state            = (known after apply)
            }
        }
    }

Plan: 2 to add, 0 to change, 1 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

google_bigquery_dataset.rh_dataset: Destroying... [id=projects/de-zoomcamp-2024-409204/datasets/demo_dataset]
google_storage_bucket.rh-bucket: Creating...
google_bigquery_dataset.rh_dataset: Destruction complete after 0s
google_bigquery_dataset.rh_dataset: Creating...
google_bigquery_dataset.rh_dataset: Creation complete after 1s [id=projects/de-zoomcamp-2024-409204/datasets/rh_dataset]
google_storage_bucket.rh-bucket: Creation complete after 1s [id=terraform-rh-terra-bucket]

Apply complete! Resources: 2 added, 0 changed, 1 destroyed.
![image](https://github.com/rahopkins/RHzoomcamp2024/assets/73754239/88c1ab8f-c9d7-474a-913f-889b68082f6a)

