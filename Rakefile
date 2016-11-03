require 'bundler/gem_tasks'
require 'appraisal'
require 'rspec/core/rake_task'

desc 'Default: run unit tests.'
task :default => [:clean, :all]

desc 'Test the paperclip plugin under all supported Rails versions.'
task :all do |t|
  exec("rm -f gemfiles/*.lock")
  Rake::Task["appraisal:gemfiles"].execute
  Rake::Task["appraisal:install"].execute
  exec('rake appraisal')
end

desc 'Test the paperclip plugin.'
RSpec::Core::RakeTask.new(:spec)

desc 'Start an IRB session with all necessary files required.'
task :shell do |t|
  chdir File.dirname(__FILE__)
  exec 'irb -I lib/ -I lib/paperclip -r rubygems -r active_record -r tempfile -r init'
end

desc 'Clean up files.'
task :clean do |t|
  FileUtils.rm_rf "doc"
  FileUtils.rm_rf "tmp"
  FileUtils.rm_rf "pkg"
  FileUtils.rm_rf "public"
  FileUtils.rm "test/debug.log" rescue nil
  FileUtils.rm "test/paperclip.db" rescue nil
  Dir.glob("paperclip-*.gem").each{|f| FileUtils.rm f }
end
