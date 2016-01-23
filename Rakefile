require 'mini_exiftool_vendored'
require 'plist'

task :export do
  from = ENV['from'] ? DateTime.parse(ENV['from']) : DateTime.now - 30
  to = ENV['to'] ? DateTime.parse(ENV['to']) : DateTime.now
  dayOneFolder = ENV["HOME"] + "/Dropbox/Apps/Day One/Journal.dayone/entries/"
  outputFolder = './DayOneExport-' + Time.now.strftime("%Y%m%d-%H%M%S")

  FileUtils.mkdir outputFolder

  Dir.glob(dayOneFolder + '*.doentry') do |entry_path|
    entry = Plist::parse_xml(entry_path)
    date = entry['Creation Date']
    includes = ENV['include'].nil? ? [] : ENV['include'].split(',')
    excludes = ENV['exclude'].nil? ? [] : ENV['exclude'].split(',')

    if date >= from and \
       date <= to and \
       (includes.empty? or (entry['Tags'] & includes).any?) and \
       (excludes.empty? or (entry['Tags'] & excludes).empty?)

      photo_path = entry_path.sub('entries', 'photos').sub('.doentry', '.jpg')
      output_path = File.join outputFolder, entry['Creation Date'].strftime("%Y%m%dT%H%M%S") + entry['UUID'][0..5] + '.jpg'

      if(File.exist? photo_path)
        FileUtils.cp photo_path, output_path
      else
        FileUtils.cp './blank.jpg', output_path
      end

      photoMetadata = MiniExiftool.new output_path

      caption = entry['Creation Date'].strftime("%^B %-d, %Y") + "\n\n" + entry['Entry Text']

      photoMetadata.imagedescription = caption
      photoMetadata.save
    end
  end
end

task :default => :export
