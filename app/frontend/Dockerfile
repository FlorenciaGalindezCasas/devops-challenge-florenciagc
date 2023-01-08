#  Especifica la imagen principal a partir de la cual está construyendo. Establece la imagen base
FROM node:16.13.0-alpine

# establece el directorio de trabajo para cualquier instrucción 
WORKDIR /app

# Copia todas las carpetas
COPY . .

# Instalacion npm
RUN npm install

# Puerto donde corre la app React
EXPOSE 3000

# Start server
CMD ["npm", "start"]


