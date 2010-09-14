ssh_user = "ziggy" # for rsync deployment
remote_root = "~/sites/iwanttoworkforcarsonified.com/public/" # for rsync deployment

common_excludes = "--exclude=Rakefile --exclude=config.rb --exclude=.sass-cache --exclude=.git --exclude=.DS_Store"

desc "Builds the site"
task :build => 'styles:clear' do
  puts "*** Building the site ***"
  system "compass compile ."
end

desc "Clears and generates new styles, builds and deploys"
task :deploy => :build do
  puts "*** Deploying the site ***"
  system("rsync -avz --chmod=Dug+rwX,o-rw,Fo-w,o+r,g+rw --delete . --exclude=src #{common_excludes} #{ssh_user}:#{remote_root}")
end

namespace :styles do
  desc "Clears the styles"
  task :clear do
    puts "*** Clearing styles ***"
    system "rm -Rfv stylesheets/*"
  end
  
  desc "Generates new styles"
  task :generate => :clear do
    puts "*** Generating styles ***"
    system "compass compile"
  end
  
end
