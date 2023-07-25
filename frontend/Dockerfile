FROM node:latest as build-stage

ARG API_URL
ARG MODE
ARG LAREX_LOCATION

ENV VITE_API_URL=${API_URL}
ENV VITE_MODE=${MODE}
ENV VITE_LAREX_LOCATION=${LAREX_LOCATION}

RUN git clone -b develop https://github.com/OCR4all/ocr4all-frontend
WORKDIR /ocr4all-frontend

RUN yarn
RUN yarn build

FROM nginx as production-stage
RUN mkdir /app
COPY --from=build-stage /ocr4all-frontend/dist /app
COPY nginx.conf /etc/nginx/nginx.conf