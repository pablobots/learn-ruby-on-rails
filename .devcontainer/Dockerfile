FROM ruby:3.2.2

# Establece el directorio de trabajo
WORKDIR /workspace

# Copia tu aplicación al contenedor (ajusta según sea necesario)
COPY . /workspace/

# Install dependencies
RUN apt-get update && \
    apt-get install -y nodejs sqlite3

# Install Rails version 3.2.2
RUN gem install rails -v '7.0.8'

# Install gemfile to start rails server
RUN bundle install --gemfile demo/Gemfile

# Install solargraph
RUN gem install solargraph

# Add non root user
ARG USERNAME=dev_user
ARG USER_UID=1000
ARG USER_GID=$USER_UID
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME
USER $USERNAME

