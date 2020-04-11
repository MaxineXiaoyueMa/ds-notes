## Returning to GCP
1. Start instance
  1. log into [console](https://console.cloud.google.com/compute/)
  2. start instance
  3. SSH into instance:
    1. `gcloud compute ssh --zone "us-west1-b" "my-fastai-instance" --project "project-name"`
    2. `gcloud compute ssh --zone=$ZONE jupyter@$INSTANCE_NAME -- -L 8080:localhost:8080`
    3. `gcloud compute ssh --zone=us-west1-b jupyter@my-fastai-instance -- -L 8080:localhost:8080`
  4. go to brower: `http://localhost:8080/tree`

2. Update course repo
  1. `cd tutorials/fastai/course-v3`
  2. `git pull`

3. Update fastai library
  1. `sudo /opt/anaconda3/bin/conda install -c fastai fastai`

4. `scp` securely copy files from gcp vm back to local: `gcloud compute scp --recurse jupyter@my-fastai-instance:~/tutorials/fastai/course-v3/nbs/dl1 /Users/max/Documents/ds-local/ds-fastai`

5. When done, **SHUT DOWN** instance!!

Reference:
1. https://cloud.google.com/sdk/gcloud/reference/compute/scp
