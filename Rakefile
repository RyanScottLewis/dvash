require 'pathname'

def require_task(path)
  begin
    require path
    
    yield
  rescue LoadError
    puts '', "Could not load '#{path}'.", 'Try to `rake gem:spec` and `bundle install` and try again.', ''
  end
end

spec = Gem::Specification.new do |s|
  
  # Variables
  s.name        = 'dvash'
  s.author      = '' # TODO
  s.email       = '' # TODO
  s.summary     = '' # TODO
  s.description = '' # TODO
  
  # Dependencies
  s.add_dependency 'parseconfig', '~> 1.0'
  s.add_dependency 'rainbow', '~> 1.1'
  s.add_dependency 'ansi', '~> 1.4'
  s.add_dependency 'service', '~> 1.0'
  s.add_dependency 'system', '~> 0.1'
  s.add_dependency 'rubigen', '~> 0.1'
  
  # Pragmatically set variables
  s.homepage = "http://github.com/codemunchies/#{s.name}"
  s.version = Pathname.glob('VERSION*').first.read
  s.require_paths = ['lib']
  s.files        = `git ls-files`.lines.to_a.collect { |s| s.strip }
  s.executables  = `git ls-files -- bin/*`.lines.to_a.collect { |s| File.basename(s.strip) }
  
end

desc 'Generate the gemspec defined in this Rakefile'
task :gemspec do
  Pathname.new("#{spec.name}.gemspec").open('w') { |f| f.write(spec.to_ruby) }
end

require_task 'rake/version_task' do
  Rake::VersionTask.new do |t|
    t.with_git_tag = true
    t.with_gemspec = spec
  end
end

require 'rubygems/package_task'
Gem::PackageTask.new(spec) do |t|
  t.need_zip = false
  t.need_tar = false
end

task :default => :gemspec