# learn-file-storage-s3-golang-starter (Tubely)

This repo contains the starter code for the Tubely application - the #1 tool for engagement bait - for the "Learn File Servers and CDNs with S3 and CloudFront" [course](https://www.boot.dev/courses/learn-file-servers-s3-cloudfront-golang) on [boot.dev](https://www.boot.dev)

## Quickstart

*This is to be used as a *reference\* in case you need it, you should follow the instructions in the course rather than trying to do everything here.

## 1. Install dependencies

- [Go](https://golang.org/doc/install)
- `go mod download` to download all dependencies
- [FFMPEG](https://ffmpeg.org/download.html) - both `ffmpeg` and `ffprobe` are required to be in your `PATH`.

```bash
# linux
sudo apt update
sudo apt install ffmpeg

# mac
brew update
brew install ffmpeg
```

- [SQLite 3](https://www.sqlite.org/download.html) only required for you to manually inspect the database.

```bash
# linux
sudo apt update
sudo apt install sqlite3

# mac
brew update
brew install sqlite3
```

- [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

## 2. Download sample images and videos

```bash
./samplesdownload.sh
# samples/ dir will be created
# with sample images and videos
```

## 3. Configure environment variables

Copy the `.env.example` file to `.env` and fill in the values.

```bash
cp .env.example .env
```

You'll need to update values in the `.env` file to match your configuration, but _you won't need to do anything here until the course tells you to_.

## 3. Run the server

```bash
go run .
```

- You should see a new database file `tubely.db` created in the root directory.
- You should see a new `assets` directory created in the root directory, this is where the images will be stored.
- You should see a link in your console to open the local web page.

## Upload layout

Uploaded thumbnails stay on the local filesystem and are served from:

- `assets/<videoID>.<ext>`

Uploaded videos are stored in S3 using an aspect-ratio prefix:

- `landscape/<random>.mp4` for 16:9 videos
- `portrait/<random>.mp4` for 9:16 videos
- `other/<random>.mp4` for videos that do not match either ratio

Before upload, videos are processed with `ffmpeg` using `-movflags faststart` so the MP4 metadata is moved to the start of the file for faster browser playback.
