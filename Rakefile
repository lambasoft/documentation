namespace :deploy do
  def deploy(env)
    puts "Building for #{env}..."
    system "TARGET=#{env} bundle exec middleman build"
    puts "Deploying to #{env}..."
    system "TARGET=#{env} bundle exec middleman s3_sync"
  end

  task :staging do
    deploy :staging
  end

  task :production do
    deploy :production
  end
end