# mutantapi

Python RESTful api  with docker for dna mutant sequence validation for Magneto recruitments.

## Local environment Requirements

- Python 3.x
- Docker
- Mysql - xampp

## Cloud environment Requirements

- AWS ElasticBeanStalk environment with Docker running on 64bit Amazon Linux 2/3.1.0
- Mysql RDS

## Tools and Installs

- docker
- python
- mysql - xampp
- jmeter - for load tests
- postman - for testing rest request


# Setup

## Local environment Python only - without docker

```bash
$ pip install -r requirements.txt
```
- Install xampp and setup up a new mysql instance
- Start apache and mysql services from xampp console
- If database is not exist yet, use emptydatabasescript/mutants.sql for importing an empty database structure to mysql
- Create a user and credentials for the new database
- Configure your 127.0.0.0:3306 as your default mysql host at db.yaml file or your own mysql host, port and credentials.
- Replace config.yaml with config-local-env-without-docker.yaml content


```bash
$ python run.py
```

## Local environment with docker

- Start apache and mysql services from xampp console
- Configure your local ip in db.yaml running ipconfig on cmd console
- Replace config.yaml with config-local-env-without-docker.yaml content

```bash
$ docker-compose build
$ docker-compose up
```



# Usage

## mutantapi urls

- Amazon AWS: -
- Local environment docker: http://127.0.0.1:5000 (use a different port in docker-compose.yml if you are running two or more services at the same time)
- Local environment without docker: http://127.0.0.1:8080

## Example request

A dna sequence as next JSON format:  

{"dna": [[string], [string], [string], ...]}  

Each string must have the same array length where this belong. The sequence only can have next chars: A, T, C, G.  

POST → /mutant/   
headers → Content-Type → application/json  
Request Body  
```json
{  
    "dna": [  
        "ATGCGA",  
        "CAGTGC",  
        "TTATGT",  
        "AGAAGG",  
        "CCCCTA",  
        "TCACTG"  
    ]  
}
```
  

## It is mutant dna response

Response Code   
200-OK  

Response Body 
```json
{  
    "isMutant": false,  
    "updatedStats": true,  
    "savedToDatabase": true  
}  
```


## It is not mutant dna response  

Response Code  
403-Forbidden  

Response Body  
```json
{    
    "isMutant": true,   
    "updatedStats": true,  
    "savedToDatabase": true  
} 
```
 



## Code Coverage

```bash
$ coverage run test_mutantvalidation.py

$ coverage report

Name                       Stmts   Miss  Cover
----------------------------------------------
mutants\__init__.py          132      5    96%
test_mutantvalidation.py      93      0   100%
----------------------------------------------
TOTAL                        225      5    98%
```

## Unit tests

```bash
$ python test_mutantvalidation.py

................
----------------------------------------------------------------------
Ran 16 tests in 4.405s

OK
```



## Performance Tests

Jmeter setup

- pending to complete

Local Jmeter load test

- pending to complete

## statsapi

Service with statistics about validated dna's

[statsapi github repository url](https://github.com/sergion2010/statsapi)

## Contributing

Pull requests are welcome. For major changes, please open an issue first, or contact me at ... to discuss what you would like to change.

Please make sure to update tests as appropriate.
