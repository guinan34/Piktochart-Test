#Basic image 
FROM ruby:3.0.6

#Get the necessary package
RUN apt-get update && apt-get install -y nodejs

#Work directory 
WORKDIR /app

#Copy the dependencies file
COPY Gemfile* .

#Install that dependencies
RUN bundle install

#Get the generated files from local to image
COPY . .

#Expose port 3000
EXPOSE 3000

#Start the server with development mode
CMD ["rails", "server", "-b", "0.0.0.0", "--environment", "{{ rails_env }}"]
