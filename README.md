# YAWC (Yet Another Web Chat)


## Development

Set some environment variables and add yawc to your Python path:

    export SECRET_KEY=somelongrandomsecret
    export DATABASE_URL=postgresql://postgres@127.0.0.1:5432
    export PYTHONPATH=$PYTHONPATH:/path/to/yawcrepodir

Install Python dependencies:

    pipenv install


Install Nodejs dependencies:

    cd web
    yarn install


Run services (PostgreSQL, Redis) via Docker:

    docker-compose up


Run database migrations:

    pipenv run alembic upgrade head


Start API server:

    pipenv run gunicorn -k flask_sockets.worker yawc.app_dev:app --reload --bind localhost:5000


Start frontend server:

    cd web
    API_URL=http://localhost:5000/graphql yarn start


Access the application by visiting http://localhost:8000

**Note:** head to http://localhost:8000/login to log in. There
currently is no redirect in place for non-authenticated users.


## User management

To create a new user:

    pipenv run python -m yawc user create 'myuser@example.com'


To list users:

    pipenv run python -m yawc user list


To change user password (for user #1 in this case):

    pipenv run python -m yawc user set-password 1
