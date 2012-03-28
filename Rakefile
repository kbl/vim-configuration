# It's importat to have set ruby to appropriate version
# appropriate version = version with which vim was build
#
# It could be checket with:
# $vim --version | grep ruby
#
# Otherwise some problems could occur with building command-t
# extension.

def my_symlink(file_name, additional_dirs='')
  destination = File.join(File.expand_path('~'), ".#{file_name}")
  source = File.join(Dir.pwd(), additional_dirs, file_name)
  if File.exists?(destination)
    puts "Symlink #{destination} exist!"
  else
    puts "Making symlink #{source} -> #{destination}"
    File.symlink(source, destination)
  end
end

task :init_submodules do
  system('git submodule init')
  system('git submodule update')
end

task :vim => :init_submodules do
  my_symlink('vimrc', 'vim')
  my_symlink('vim')
  Dir.chdir(File.join(%w(vim bundle command-t))) do
    system('rake make')
    system('make install')
  end
end

task :git do
  my_symlink('gitconfig')
  my_symlink('gitignore')
end

task :default => [:vim, :git]

