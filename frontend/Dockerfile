FROM node:18-alpine AS build
WORKDIR /app
ARG REACT_APP_API_URL=https://demo.eminencetechsolutions.com:3063
ARG REACT_APP_WS_URL=wss://demo.eminencetechsolutions.com:3063
ENV REACT_APP_API_URL=$REACT_APP_API_URL
ENV REACT_APP_WS_URL=$REACT_APP_WS_URL
COPY package*.json ./
RUN npm install --legacy-peer-deps
COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80 443
CMD ["nginx", "-g", "daemon off;"]
