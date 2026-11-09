# Vibefy – Music Streaming Web Application

Vibefy is a Django-based music application for browsing songs, artists, and genres, playing audio, uploading music, and managing favorite songs. It also exposes REST API endpoints for music data and JWT-based API authentication.

## Features

- **User accounts:** Register, log in, and log out through the web interface.
- **JWT authentication:** API registration, login/token generation, and token refresh endpoints.
- **Music library:** Browse songs, artists, and genres.
- **Audio playback:** Play song files using AmplitudeJS, with WaveSurfer included for waveform display.
- **Song uploads:** Authenticated users can upload an audio file and cover image, and provide song details.
- **Audio metadata:** TinyTag is used to read audio duration and file size during upload.
- **Favorites:** Logged-in users can mark songs as favorites or remove them from favorites.
- **REST API:** Endpoints for songs, artists, genres, artist details, and songs by genre.

> **Scope note:** The code includes a `free`/`paid` song type and a price field, but the repository does not show a payment-processing integration. Do not describe paid purchases as an implemented feature.

## Tech Stack

| Area | Technology |
|---|---|
| Backend | Python, Django |
| REST APIs | Django REST Framework |
| API authentication | Django REST Framework SimpleJWT |
| Database configured in Django settings | SQLite |
| Frontend | Django templates, HTML, CSS, JavaScript, jQuery |
| Audio playback / waveform | AmplitudeJS, WaveSurfer |
| Audio metadata | TinyTag |
| Image handling | Pillow |
| Container setup | Docker, Docker Compose |

The project uses Django templates and static frontend assets; it is **not a React application**.

## Project Structure

```text
Vibefy/
├── accounts/           # Custom user model, account views and authentication APIs
│   └── api/             # Registration and JWT API endpoints
├── core/                # Songs, artists, genres, favorites and related views
│   └── api/             # Music REST API endpoints and serializers
├── music/               # Django project settings, root URLs and WSGI config
├── templates/           # Django HTML templates
├── static/              # CSS, JavaScript, fonts and static images
├── media/               # Uploaded song files and images (runtime data)
├── utils/               # Song-related helper functions
├── manage.py
├── requirements.txt
├── Dockerfile
├── docker-compose.yml
└── LICENSE
```

## Getting Started

### Prerequisites

- Python compatible with the dependency versions in `requirements.txt`
- pip
- Git

### 1. Clone the repository

```bash
git clone https://github.com/Raghavchaw/Vibefy.git
cd Vibefy
```

### 2. Create and activate a virtual environment

**macOS / Linux**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

**Windows (PowerShell)**

```powershell
py -m venv .venv
.venv\Scripts\Activate.ps1
```

### 3. Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Apply database migrations

```bash
python manage.py migrate
```

### 5. Run the development server

```bash
python manage.py runserver
```

Open `http://127.0.0.1:8000/` in your browser.

## API Endpoints

The API routes are mounted under `/v1/api/`.

| Method | Endpoint | Purpose |
|---|---|---|
| GET | `/v1/api/default` | Retrieve a default free song |
| GET | `/v1/api/home` | Retrieve song data for the home API |
| GET | `/v1/api/songs` | List songs |
| GET | `/v1/api/songs/<id>` | Retrieve a song |
| GET | `/v1/api/artists` | List artists |
| GET | `/v1/api/artists/<slug>` | Retrieve an artist and associated songs |
| GET | `/v1/api/genres` | List genres |
| GET | `/v1/api/genres/<id>/songs` | List songs for a genre |
| POST | `/v1/api/accounts/register/` | Register an API user |
| POST | `/v1/api/accounts/login/` | Obtain JWT access and refresh tokens |
| POST | `/v1/api/accounts/token/refresh/` | Refresh a JWT access token |

For protected API requests, send the access token using the Bearer authorization scheme:

```http
Authorization: Bearer <access-token>
```

## Docker

The repository includes a `Dockerfile` and Docker Compose configuration. Review the database configuration before using the Compose setup: the checked-in Django settings configure SQLite, while `docker-compose.yml` also defines a PostgreSQL service. The Compose file does not, by itself, make Django use that PostgreSQL service.

## Configuration and Security Notes

Before deploying or publishing this project:

- Move `SECRET_KEY` out of `music/settings.py` and load it from an environment variable.
- Set `DEBUG = False` in production.
- Replace `ALLOWED_HOSTS = ["*"]` with the actual hostnames.
- Review database, static-file, and media-file settings for the deployment environment.
- Do not commit local databases, private environment files, or user-uploaded media unless they are intentionally included and safe to publish.
- Check the dependency versions in `requirements.txt` for compatibility with the Python version used to run the project.

## License

See the [LICENSE](LICENSE) file for license information.

## Author

**Raghav Chawla**  
GitHub: [@Raghavchaw](https://github.com/Raghavchaw)
