FROM denoland/deno:alpine-2.1.1

WORKDIR /app
COPY deno.* .
RUN deno install
COPY . .
EXPOSE 3000
