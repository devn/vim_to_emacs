#!/usr/bin/env ruby

class VimInfoParser

  # $DO_NOT_OPEN = [/.*\/\.git\/.*$/]
  $OUTPUT_FILE = File.expand_path("~/.vim_to_emacs")

  def initialize()
    viminfo = File.open( File.expand_path("~/.viminfo"), 'r') do |f|
      f.read
    end

    return_jumplist( viminfo )
  end

  def return_jumplist(viminfo_contents)
    extract_file_paths( viminfo_contents.split(/^# Jumplist.*$/)[1].split(/^# History.*$/)[0].split(/\n/) )
  end


  def extract_file_paths(content_strings)
    file_paths=[]

    content_strings.each do |line|
      line =~ /^.*(~\/.*)$/
      path = $1

      unless line =~ /.*\/\.git\/.*$/
        file_paths << path
      end
    end

    write_paths( file_paths.reject { |n| n.nil? }.uniq )
  end

  def write_paths(file_strings)
    File.open($OUTPUT_FILE, 'w') do |f|
      file_strings.each do |path|
        f.write "#{File.expand_path(path)}\n"
      end
    end
    construct_file_type_hash
  end

  # TODO: Look into emacsclient options for the way I want to open
  # files vs directories
  def open_directories
    @open_me[:directories].each do |d|
      `emacsclient -c #{d}`
    end
  end

  def open_files
    @open_me[:files].each do |f|
      `emacsclient -c #{f}`
    end
  end

  def construct_file_type_hash
    files_arr = File.readlines(File.expand_path("~/.vim_to_emacs"), "r+").to_s.split(/\n/)
    
    directories = files_arr.select { |f| File.directory?(f) }
    files = files_arr.select { |f| File.file?(f) }

    @open_me = {:directories => directories.to_a, :files => files}
  end

  # TODO: Implement regex blacklist
  # def blacklist_check(unique_entries)
  #   unique_entries.reject do |entry|
  #     $DO_NOT_OPEN.each do |regex|
  #       entry =~ regex
  #     end
  #   end
  # end

end

go = VimInfoParser.new

go.open_directories
go.open_files


