FROM golang:1.22-alpine AS BUILDER

WORKDIR /usr/src/app

COPY . .

RUN go mod download

RUN go build -o product-catalog ./

ENV PRODUCT_CATALOG_PORT=8088

ENTRYPOINT [ "./product-catalog" ]