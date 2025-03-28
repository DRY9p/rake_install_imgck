require 'rake/clean'

task :clone_from_repo do
  sh "git clone https://github.com/ImageMagick/ImageMagick"
end

task :install_imgck => :clone_from_repo do
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

task :rm_imgck
  sh "rm -rf ImageMagick"
end