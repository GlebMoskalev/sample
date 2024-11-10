# Используем базовый образ .NET SDK для сборки приложения
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

# Устанавливаем рабочую директорию
WORKDIR /app

# Копируем файл проекта (csproj) и восстанавливаем зависимости
COPY *.csproj ./
RUN dotnet restore

# Копируем все файлы проекта и выполняем публикацию
COPY . ./
RUN dotnet publish -c Release -o out

# Используем базовый образ ASP.NET для запуска приложения
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime

# Устанавливаем рабочую директорию
WORKDIR /app

# Копируем опубликованные файлы из стадии сборки
COPY --from=build /app/out ./

# Открываем порт, на котором будет работать приложение
EXPOSE 8080

# Задаем точку входа для запуска приложения
ENTRYPOINT ["dotnet", "BlazorApp3.dll"]