require 'tata'

@config = Tata::Config::Defaults

task :default => :new

desc "Create a new article."
task :new do
  title = ask('Title: ')
  slug = title.empty?? nil : title.strip.slugize

  article = {'title' => title, 'date' => Time.now.strftime("%d/%m/%Y")}.to_yaml
  article << "\n"
  article << "Once upon a time...\n\n"

  path = "#{Tata::Paths[:articles]}/#{Time.now.strftime("%Y-%m-%d")}#{'-' + slug if slug}.#{@config[:ext]}"

  unless File.exist? path
    File.open(path, "w") do |file|
      file.write article
    end
    tata "an article was created for you at #{path}."
  else
    tata "I can't create the article, #{path} already exists."
  end
end

desc "Publish my blog."
task :publish do
  tata "publishing your article(s)..."
  `git push heroku master`
end

def tata msg
  puts "\n  tata ~ #{msg}\n\n"
end

def ask message
  print message
  STDIN.gets.chomp
end
