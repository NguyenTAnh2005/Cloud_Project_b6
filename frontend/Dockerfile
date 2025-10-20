# FROM node:20-alpine AS build - Up nhieu nhung bi loi 
#target frontend: failed to solve: failed to fetch anonymous token: unexpected status from GET request to
#https://auth.docker.io/token?scope=repository%3Alibrary%2Fnode%3Apull&service=registry.docker.io: 503 Service Unavailable
FROM ghcr.io/nodejs/node:20-alpine AS build
WORKDIR /app
COPY package.json package-lock.json* pnpm-lock.yaml* yarn.lock* .npmrc* ./ 2>/dev/null || true
RUN npm install
COPY . .
RUN npm run build

FROM nginx:1.27-alpine
COPY --from=build /app/dist /usr/share/nginx/html
RUN rm /etc/nginx/conf.d/default.conf || true
COPY nginx.conf /etc/nginx/conf.d/app.conf
EXPOSE 80
CMD ["nginx","-g","daemon off;"]
