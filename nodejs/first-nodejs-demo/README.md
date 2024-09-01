# Notes

## CommonJS & ECMAScript Modules System
CommonJS uses `require` and `module.exports` to import and export modules. ECMAScript Modules uses `import` and `export` to import and export modules.

Node.js handles `.cjs` files as CommonJS modules and `.mjs` files as ECMAScript modules. For `.js` files, it uses the project's default module system, which is CommonJS unless the package.json specifies `"type": "module"`.

## Docker File Explanation
```
FROM node:14

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 3000

CMD [ "node", "app.mjs" ]
```

- `FROM node:14`: Grab node environment from Docker Hub, use the official Node.js 14 image as the base image. 
- `WORKDIR /app`: Set the working directory to `/app`.
- `COPY package.json .`: Copy the `package.json` file to the working directory (`/app`).
- `RUN npm install`: Install the dependencies.
- `COPY . .`: Copy the rest of the files to the working directory.
- `EXPOSE 3000`: Expose port 3000.
- `CMD [ "node", "app.mjs" ]`: Run the `app.mjs` file when the container starts.

## Docker Commands
Build the image based on Dockerfile:
```
>> docker build .
```

Run the container:
```
>> docker run -p 3000:3000 <image-id>
```
The first 3000 is the host port, and the second 3000 is the container port.  
So, `-p 3000:3000` maps port 3000 on the host machine to port 3000 inside the Docker container. This allows you to access the application running inside the container on port 3000 from your host machine by navigating to http://localhost:3000.

List the container:
```
>> docker ps
```

Stop the container:
```
>> docker stop <container-id>
or
>> docker stop <container-name>
```
