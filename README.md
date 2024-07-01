# AWS
## Step 1: Update and Install Dependencies
```bash
sudo apt update
sudo apt install -y gcc gcc-c++ git
sudo apt install -y python3 python3-pip python3-devel

sudo pip3 install virtualenv

virtualenv airflow_env
source airflow_env/bin/activate

export AIRFLOW_HOME=~/airflow
pip install apache-airflow
pip install pandas openpyxl ray[tune] neuralforecast

airflow db init

airflow users create \
    --username admin \
    --firstname FIRST_NAME \
    --lastname LAST_NAME \
    --role Admin \
    --email admin@example.com \
    --password yourpassword

mkdir -p ~/airflow/dags

scp -i /path/to/your-key.pem nixtla_automate.py ec2-user@your-ec2-public-dns:~/airflow/dags/

airflow webserver --port 8080
```
#### In a new terminal session, start the Airflow scheduler:
```bash
ssh -i /path/to/your-key.pem ec2-user@your-ec2-public-dns

source airflow_env/bin/activate
airflow scheduler
```
### Open your web browser and navigate to http://your-ec2-public-dns:8080.
Log in with the user credentials you created (admin).
