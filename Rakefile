require "rubygems"
require "bundler/setup"
require "stringex"

# This will be configured for you when you run config_deploy
deploy_branch  = "master"
deploy_dir      = "_site"   # deploy directory (for Github pages deployment)
public_dir = "public"

desc "deploy public directory to github pages"
multitask :push do
  (Dir["#{public_dir}/*"]).each { |f| rm_rf(f) }
  Rake::Task[:copydot].invoke(deploy_dir, public_dir)
  puts "\n## copying #{deploy_dir} to #{public_dir}"
  cp_r "#{deploy_dir}/.", public_dir
  puts "## Deploying branch to Github Pages "
  cd "#{public_dir}" do
    system "git add ."
    system "git add -u"
    puts "\n## Commiting: Site updated at #{Time.now.utc}"
    message = "Site updated at #{Time.now.utc}"
    system "git commit -m \"#{message}\""
    puts "\n## Pushing generated #{public_dir} website"
    system "git push origin #{deploy_branch} --force"
    puts "\n## Github Pages deploy complete"
  end
end

desc "copy dot files for deployment"
task :copydot, :source, :dest do |t, args|
  FileList["#{args.source}/**/.*"].exclude("**/.", "**/..", "**/.DS_Store", "**/._*").each do |file|
    cp_r file, file.gsub(/#{args.source}/, "#{args.dest}") unless File.directory?(file)
  end
end
