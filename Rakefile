require "rubygems"
require "bundler/setup"
require "stringex"

# This will be configured for you when you run config_deploy
deploy_branch  = "master"
deploy_dir      = "_site"   # deploy directory (for Github pages deployment)

desc "deploy public directory to github pages"
task :push do
  puts "## Deploying branch to Github Pages "
  cd "#{deploy_dir}" do
    system "git add ."
    system "git add -u"
    puts "\n## Commiting: Site updated at #{Time.now.utc}"
    message = "Site updated at #{Time.now.utc}"
    system "git commit -m \"#{message}\""
    puts "\n## Pushing generated #{deploy_dir} website"
    system "git push origin #{deploy_branch} --force"
    puts "\n## Github Pages deploy complete"
  end
end