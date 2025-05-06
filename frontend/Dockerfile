#Use Bun base image
FROM oven/bun:1.0-alpine

#set working directory
WORKDIR /app

#copy package.json and install dependencies
COPY package.json package-lock.json ./
RUN bun install

#copy the rest of the app
COPY . .

#export the port 5173 for Vite
EXPOSE 5173

#satrt Vite dev server witch Bun
CMD ["bun", "run", "dev", "--", "--host", "0.0.0.0"]