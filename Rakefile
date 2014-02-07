_, ROOT = Rake.application.find_rakefile_location

Dir[ROOT + '/tasks/**/*.rake'].each do |tasks|
  load File.expand_path( tasks )
end

task :default => :help

namespace :ci do

  namespace :spec do

    desc 'Run rspec-puppet formatted for Jenkins'
    task :unit do
      ENV['SPEC_FORMAT'] = '-r yarjuf -f JUnit -o unit_results.xml -fd'
      Rake::Task['spec:unit'].invoke
    end

    desc 'Run beaker-rspec formatted for Jenkins'
    task :system do
      ENV['SPEC_FORMAT'] = ''
      Rake::Task['spec:system'].invoke
    end
  end

  desc 'Lint Puppet style with puppet-lint formatted for Jenkins'
  task :lint do
    ENV['LINT_FORMAT'] = '%{path}:%{linenumber}:%{check}:%{KIND}:%{message}'
    Rake::Task['lint'].invoke
  end
end

