FROM ruby:2.6-alpine

ENV APP_HOME /app
RUN mkdir $APP_HOME
WORKDIR $APP_HOME

COPY Gemfile* $APP_HOME/
RUN apk add --no-cache --update ruby-dev build-base \
    && gem install bundler \
    && bundle install \
    && apk del ruby-dev build-base \
    && rm -rf /var/cache/apk/*

COPY . $APP_HOME

ENV COMMENT_DATABASE_HOST comment_db
ENV COMMENT_DATABASE comments

CMD ["puma"]
