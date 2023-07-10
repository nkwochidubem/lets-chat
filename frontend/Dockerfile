FROM node:16.20.1-alpine AS development

ENV CI=true
ENV PORT=3000

WORKDIR /code
COPY frontend/package.json /code/package.json
COPY frontend/yarn.lock /code/yarn.lock

#RUN npm i -g yarn@latest

RUN yarn install --production

COPY frontend/. /code

CMD [ "npm", "start" ]

#FROM development AS builder

#RUN npm run build

#FROM nginx:1.13-alpine

#COPY --from=builder /code/build /usr/share/nginx/html
