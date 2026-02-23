# /////////  Create non Root User in Dockerfile //////////

# FROM node:25

# WORKDIR /app

# # Create non-root user
# RUN groupadd -r appuser && useradd -r -g appuser appuser

# COPY . .

# RUN npm install

# # Switch to non-root user
# USER appuser

# EXPOSE 3000

# CMD ["npm", "start"]

# ////////////////////////////////////////////////////////


# /////////////  Use Multi-Stage Build for Smaller Image Size /////////////

FROM node:25 AS builder

WORKDIR /builder

COPY package*.json ./

RUN npm install

COPY . .

# -------- Runtime Stage --------
FROM gcr.io/distroless/nodejs20-debian12

FROM node:25-slim

WORKDIR /app

COPY --from=builder /builder/node_modules ./node_modules
COPY --from=builder /builder/app.js ./app.js

EXPOSE 3000

CMD ["node", "app.js"]