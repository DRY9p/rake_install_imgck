require 'rake/clean'
require 'nokogiri'
require 'pry'

def extract_from_html
  html_content = File.open('current_version_site.html')
  doc = Nokogiri::HTML(html_content)

  extract_code_links(doc)
end

def extract_code_links(doc)
  content = doc.css('pre.p-3.mb-2.text-body-secondary').children.inner_html
  
  content.split("\n").reject{ |line| line.empty?}
  binding.pry
end

task :parse_command do
  site_url = "https://imagemagick.org/script/install-source.php"
  sh "curl -s #{site_url} > current_version_site.html"
  puts "Создан current_version_site.html"
end

task :install_imgck => :parse_command do
  extract_from_html.each do |command|
    problem_resolver(command)
  end
end

def problem_resolve(command)
  begin
    puts "Выполнение: #{command}"
    sh command
  rescue => e
    puts "Ошибка при выполнении:#{command} - #{e.message}"
  
    puts "❌ Требуется установить ImageMagick для проверки версии!" if command.include?('magick identify')
    
    if command.include?('./configure')
      puts "Выполнение #{command} внутри директории ImageMagick"
      Dir.chdir("ImageMagick") do
        sh command
      end
    end

    if command.include?('git clone')
      puts "⏳ Решение проблемы с #{e.message}"
      sh "git clone https://github.com/ImageMagick/ImageMagick"
    end
  end
end