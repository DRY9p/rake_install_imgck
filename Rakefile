# frozen_string_literal: true

require 'rake/clean'

# ImageMagick installation
task :clone_imgck_repo do
  sh 'git clone https://github.com/ImageMagick/ImageMagick'
end

task imgck_install: :clone_imgck_repo do
  Dir.chdir('ImageMagick') do
    sh './configure'
    system 'sudo make install'
    system 'sudo ldconfig /usr/local/lib'
    sh '/usr/local/bin/magick logo: logo.gif'
    sh 'make check'
  rescue StandardError => e
    puts "Ошибка при выполнении #{e.message}"
  end
end

task :rm_imgck do
  system('sudo rm -rf ImageMagick')
end

# Vips installation & additing configuration dynamic lib file
task :libvips_install do
  ['sudo apt update',
   'sudo apt-get -y install libvips-dev',
   'sudo apt update'].each { |command| system(command) }
end

# Solidus installation
task :solidus_install  do
  # additional arguments to versions ignoring task name
  args = ARGV[1..-1]

  system 'sudo apt-get install nodejs'
  sh "rbenv global #{args[0]}" # 3.3.7
  sh "rails _#{args[1]}_ new #{args[2]}" # 7.2.2.1

  Dir.chdir(args[2]) do
    sh 'mkdir -p app/assets/config'
    sh 'cat <<MANIFEST > app/assets/config/manifest.js
//= link_tree ../images
//= link_directory ../javascripts .js
//= link_directory ../stylesheets .css
MANIFEST'

    sh 'bundle add solidus'
    sh 'bin/rails g solidus:install'
  end
end
