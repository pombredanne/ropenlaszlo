# Copyright (c) 2006 Oliver Steele <steele@osteele.com>
# All rights reserved.
# 
# This program is free software.
# This file is distributed under an MIT style license.  See
# MIT-LICENSE for details.

require 'rubygems'
require 'rake/gempackagetask'

PKG_NAME = "ropenlaszlo"
PKG_VERSION = '0.2.0'
RUBYFORGE_PROJECT = 'ropenlaszlo'

PKG_FILES = FileList['{lib,doc,test}/**/*'].exclude('.svn')

spec = Gem::Specification.new do |s|
  s.name = PKG_NAME
  s.version = PKG_VERSION
  s.summary = "Ruby interface to OpenLaszlo."
  s.author = 'Oliver Steele'
  s.email = 'steele@osteele.com'
  s.homepage = 'http://ropenlaszlo.rubyforge.org'
  s.rubyforge_project = RUBYFORGE_PROJECT
  s.require_path = 'lib'
  s.files = PKG_FILES
  s.description = <<-EOF
    ROpenLaszlo is an interface to the OpenLaszlo compiler.
EOF
  s.has_rdoc = true
  s.extra_rdoc_files = FileList['doc/*']
  s.rdoc_options << '--title' <<
    'ROpenLaszlo -- Ruby interface to OpenLaszlo' <<
    '--main' << 'doc/README'
end

Rake::GemPackageTask.new(spec) do |pkg|
  pkg.need_zip = true
  pkg.need_tar = true
end

task :test_install do
  sh "gem uninstall ropenlaszlo"
  sh "gem install pkg/ropenlaszlo"
end

task :clean do
  rm_rf 'pkg'
end

# Adapted from Typo's Rakefile
desc "Publish the release files to RubyForge."
task :tag_svn do
  url = `svn info`[/^URL:\s*(.*\/)trunk/, 1]
  system("svn cp #{url}/trunk #{url}/tags/release_#{PKG_VERSION.gsub(/\./,'_')} -m 'tag release #{PKG_VERSION}'")
end
