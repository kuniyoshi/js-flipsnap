repo = 'git@github.com:pxgrid/js-flipsnap.git'
site_dir = '_site'
deploy_dir = '_deploy'

desc 'setup gh-pages'
task 'setup' do
  rm_rf deploy_dir
  sh "git clone #{repo} #{deploy_dir}"
  cd "#{deploy_dir}" do
    sh 'git checkout -b gh-pages origin/gh-pages'
  end
end

desc 'deply to gh-pages'
task 'deploy' do
  unless Dir.exists? deploy_dir
    puts 'deploy dir is not created. try this.'
    puts '$ rake setup'
    next
  end

  Dir["#{deploy_dir}/*"].each { |f| rm_rf(f) }
  cp_r "#{site_dir}/.", deploy_dir
  cd "#{deploy_dir}" do
    sh 'git add -A'
    puts "\n## Commiting: Site updated at #{Time.now.utc}"
    message = "Site updated at #{Time.now.utc}"
    sh "git commit -m \"#{message}\""
    puts "\n## Pushing generated #{deploy_dir} website"
    sh "git push origin gh-pages --force"
    puts "\n## Github Pages deploy complete"
  end
end
