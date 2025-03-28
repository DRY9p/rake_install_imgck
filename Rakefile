require 'rake/clean'

# ImageMagick installation
task :clone_imgck_repo do
  sh "git clone https://github.com/ImageMagick/ImageMagick"
end

task :imgck_install => :clone_imgck_repo do
  Dir.chdir("ImageMagick") do
    begin
      sh "./configure"
      sh "sudo make install"
      sh "sudo ldconfig /usr/local/lib"
      sh "/usr/local/bin/magick logo: logo.gif"
      sh "make check"
    rescue => e
      puts "Ошибка при выполнении #{e.message}"
    end
  end
end

task :rm_imgck do
  sh "rm -rf ImageMagick"
end

# Brew installation & configure .bash_profile
task :brew_install do
  sh '/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"'
end

task :brew_profile => :brew_install do
  sh 'echo >> /home/cr9co0/.bashrc'
  system('echo \'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"\' >> /home/cr9co0/.bashrc')
  sh 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"'
  sh 'sudo apt-get install build-essential'
end

# Vips installation & additing configuration dynamic lib file
task :vips_install => :brew_install do
  sh 'brew install vips'
  # проверка наличиля либ в директории
  sh 'ls -l /home/linuxbrew/.linuxbrew/lib/libvips*'
  # создаем файл конфигурации для динамического загрузчика системных либ
  # (p.s они все работают через brew по пути /home/linuxbrew/.linuxbrew/lib :) )
  system('echo \'/home/linuxbrew/.linuxbrew/lib\' | sudo tee /etc/ld.so.conf.d/vips.conf')
  # обновляем кэш библиотек
  sh 'sudo ldconfig'
end

# Solidus installation
task :solidus_install => [:imgck_install, :vips_install] do 
  sh 'bundle add solidus'
  sh 'bin/rails g solidus:install'
end