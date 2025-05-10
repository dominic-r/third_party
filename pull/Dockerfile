FROM denoland/deno:alpine-2.1.1@sha256:89b558df4099d2df373412f0a4cbfb6b30f5ddeeb7154b6f439b033fe1d646cd

WORKDIR /app
COPY deno.* .
RUN deno install
COPY . .
EXPOSE 3000
