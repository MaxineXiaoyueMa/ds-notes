## Returning to GCP
1. Start instance
   1. if fail to start due to 'not enough resource', see [troubleshoot](#troubleshoot-not-enough-resource)
   1. log into [console](https://console.cloud.google.com/compute/)
   2. start instance
   3. SSH into instance:
    1. `gcloud compute ssh --zone "us-west1-b" "my-fastai-instance" --project "project-name"`
    2. `gcloud compute ssh --zone=$ZONE jupyter@$INSTANCE_NAME -- -L 8080:localhost:8080`
    3. `gcloud compute ssh --zone=us-west1-b jupyter@my-fastai-instance -- -L 8080:localhost:8080`
    4. go to browser: `http://localhost:8080/tree`

2. Update course repo
  1. `cd tutorials/fastai/course-v3`
  2. `git pull`

3. Update fastai library
  1. `sudo /opt/anaconda3/bin/conda install -c fastai fastai`

4. `scp` securely copy files from gcp vm back to local: `gcloud compute scp --recurse jupyter@my-fastai-instance-v20200528:~/tutorials/fastai/course-v3/nbs/dl1/lesson3-imdb-max-v20200528.ipynb /Users/max/Documents/ds-local/ds-fastai --zone "us-east1-b"`


5. When done, **SHUT DOWN** instance!!

## Troubleshoot not enough resource
1. Try to retry
2. Create a new instance
  ```shell
  export IMAGE_FAMILY="pytorch-latest-gpu" # or "pytorch-latest-cpu" for non-GPU instances
  export ZONE="us-east1-b" #or try other zones us-west1-a/b, us-central1-c/f, us-east1-b/c
  export INSTANCE_NAME="my-fastai-instance-v20200528" # add a date for easy reference
  export INSTANCE_TYPE="n1-highmem-8" # budget: "n1-highmem-4"

  # budget: 'type=nvidia-tesla-T4,count=1'
  gcloud compute instances create $INSTANCE_NAME \
          --zone=$ZONE \
          --image-family=$IMAGE_FAMILY \
          --image-project=deeplearning-platform-release \
          --maintenance-policy=TERMINATE \
          --accelerator="type=nvidia-tesla-p100,count=1" \
          --machine-type=$INSTANCE_TYPE \
          --boot-disk-size=200GB \
          --metadata="install-nvidia-driver=True" #\
          #--preemptible #disable preemptible when unstable
    ```


## Reference
1. Google official document: https://cloud.google.com/sdk/gcloud/reference/compute/scp
2. Troubleshoot question on stackoverflow: https://stackoverflow.com/questions/52684656/the-zone-does-not-have-enough-resources-available-to-fulfill-the-request-the-re
3. fastai setup guide: https://course.fast.ai/start_gcp.html
