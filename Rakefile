require "fileutils"
require "tmpdir"

FONTCONFIG_PACKAGE_TGZ = ENV['FONTCONFIG_PACKAGE_TGZ']

desc "download Fontconfig"
task "fontconfig:download", :version do |t, args|
  version = args[:version]

  sh "curl http://www.freedesktop.org/software/fontconfig/release/fontconfig-#{version}.tar.gz -s -o - | tar vzxf -"
end

desc "install Fontconfig"
task "fontconfig:build", :version do |t, args|
  version = args[:version]
  name    = "fontconfig-#{version}"
  prefix  = "/app/vendor/#{name}"

  build_command = [
    "./configure --disable-static --disable-docs --prefix=#{prefix}",
    "make",
    "make install",
  ].join(" && ")

  sh "vulcan build -v -o #{name}.tgz --source #{name} --prefix=#{prefix} --command=\"#{build_command}\""

  puts "Vulcan is done with #{name}. Upload now #{name}.tgz to Amazon S3."
  puts "Set the environment variable FONTCONFIG_PACKAGE_TGZ to the online location of fontconfig."
end

desc "download Poppler"
task "poppler:download", :version do |t, args|
  version = args[:version]

  sh "curl http://poppler.freedesktop.org/poppler-#{version}.tar.gz -s -o - | tar vzxf -"
end

desc "install Poppler"
task "poppler:build", :version do |t, args|
  version = args[:version]
  name    = "poppler-#{version}"
  prefix  = "/app/vendor/#{name}"

  build_command = [
    "./configure --disable-static --enable-zlib --prefix=#{prefix}",
    "make",
    "make install",
  ].join(" && ")

  sh "vulcan build -v -d #{ENV['FONTCONFIG_PACKAGE_TGZ']} -o #{name}.tgz --source #{name} --prefix=#{prefix} --command=\"#{build_command}\""

  puts "Vulcan is done with #{name}. Upload now #{name}.tgz to Amazon S3."
end
