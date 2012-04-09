site_dir = '_site'
deploy_dir = '_deploy'

desc 'deply to gh-pages'
task 'deploy' do
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
