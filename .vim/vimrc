call plug#begin('~/.vim/plugged')

Plug '/usr/local/opt/fzf'
Plug 'junegunn/fzf.vim'
Plug 'scrooloose/nerdtree'
Plug 'rking/ag.vim'
Plug 'godlygeek/tabular'
Plug 'zerowidth/vim-copy-as-rtf'
Plug 'terryma/vim-multiple-cursors'
Plug 'sheerun/vim-polyglot'
Plug 'tpope/vim-rails'
Plug 'ap/vim-css-color'
Plug 'jayflo/vim-skip'
Plug 'SirVer/ultisnips'
Plug 'honza/vim-snippets'
Plug 'tmhedberg/matchit'
Plug 'tomtom/tcomment_vim'
Plug 'itchyny/lightline.vim'
Plug 'mhartington/oceanic-next'
Plug 'henrik/vim-indexed-search'

call plug#end()

" Color scheme
if filereadable(expand("$HOME/.vim/plugged/oceanic-next/colors/OceanicNext.vim"))
  syntax enable
  " for vim 7
  set t_Co=256


  " for vim 8
  if (has("termguicolors"))
    set termguicolors
  endif

  let g:oceanic_next_terminal_bold = 1
  let g:oceanic_next_terminal_italic = 1

  colorscheme OceanicNext
endif

" Main configurations
set nocompatible

set colorcolumn=80
set hidden
set wrap        " wrap lines
set tabstop=2
set shiftwidth=2
set softtabstop=2
set tabpagemax=20
set showtabline=2
set smarttab
set smartindent
set expandtab
set backspace=indent,eol,start
                  " allow backspacing over everything in insert mode
set autoindent    " always set autoindenting on
set copyindent    " copy the previous indentation on autoindenting
set number        " always show line numbers
set numberwidth=5
set shiftround    " use multiple of shiftwidth when indenting with '<' and '>'
set showmatch     " set show matching parenthesis
set ignorecase    " ignore case when searching
set smartcase     " ignore case if search pattern is all lowercase,
                  "    case-sensitive otherwise
set smarttab      " insert tabs on the start of a line according to
                  "    shiftwidth, not tabstop
set hlsearch    " highlight search terms
set incsearch     " show search matches as you type
set title
set visualbell           " don't beep
set noerrorbells         " don't beep
set history=1000         " remember more commands and search history
set undolevels=1000      " use many levels of undo
set undofile  "Maintain undo history between sessions
set undodir=~/.vim/undodir
set nobackup
set noswapfile " Don't create swap file
set nowritebackup
set autoread " Load file when change
set guioptions-=r " Removes right hand scroll bar
set clipboard+=unnamed
set mouse=a
set ttymouse=xterm2
set wildmenu "Better popup menu
set confirm "Dialog to ask when closing unsave changes
set nofoldenable " disable folding

"Disable sounds and screen flashing
set visualbell
set t_vb=

"May be improve the speed
set lazyredraw
set ttyfast

" Wildignore
set wildignore+=*.o,*.obj,system*,*.svg,*.ttf,*.eot,*.jpg,*.png,*.gif,*.log,tmp,yard_templates,coverage
set list listchars=tab:»·,trail:·

" Encoding
set encoding=utf-8
set fileencoding=utf-8
set fileencodings=utf-8

" show tab number
au BufRead,BufNewFile * set guitablabel=%N.\ %t\ %M

" Leader key
let mapleader=","

" Mapping

" ctrl+tab to next tab
noremap <c-tab> :tabnext<cr>
noremap tn :tabnew<cr>

" Map tabs command + number
nmap <D-1> 1gt<cr>
nmap <D-2> 2gt<cr>
nmap <D-3> 3gt<cr>
nmap <D-4> 4gt<cr>
nmap <D-5> 5gt<cr>
nmap <D-6> 6gt<cr>
nmap <D-7> 7gt<cr>
nmap <D-8> 8gt<cr>
nmap <D-9> 9gt<cr>
nmap <D-[> gT
nmap <D-]> gt
nmap <D-0> :tablast<CR>

" Nohl
nmap <c-h> :nohl<cr>

function! GithubCopyLineUrl()
  let line1 = a:firstline
  let line2 = a:lastline
  let commit = substitute(system('git rev-parse HEAD'), '[\]\|[[:cntrl:]]', '', 'g')
  let cmd = 'git ls-remote --get-url | sed "s/:/\//g" | sed "s/git@/https:\/\//g" | sed "s/\.git/\/blob\//g"'
  let result = substitute(system(cmd), '[\]\|[[:cntrl:]]', '', 'g')

  if line1 != line2
    let lines = '#L' . line1 . '-L' . line2
  else
    let lines = '#L' . line1
  endif

  let @*=(result . commit . '/' . expand("%") . lines)
endfunction

nmap <Leader>cs :let @*=expand("%")<CR>
nmap <Leader>cl :let @*=expand("%:p")<CR>
nmap <Leader>cr :let @*=('rspec ' . expand("%") . ':' . line("."))<CR>
nmap <Leader>cg :call GithubCopyLineUrl()<CR>
vnoremap <Leader>cg :call GithubCopyLineUrl()<CR>

" Alias to save and quit
command WQ wq
command Wq wq
command W w
command Q q
command QA qa
command Qa qa

" Set FileTypes
nmap <Leader>ftr :set ft=ruby<CR>

" Remove trailing whitespace
au BufWritePre * :%s/\s\+$//e

" File identation
au FileType xml setlocal equalprg=xmllint\ --format\ --recover\ -\ 2>/dev/null
au FileType json setlocal equalprg=python\ -m\ json.tool

" Custom commands
command! -range=% RubyNewHashNotation silent execute <line1>.','.<line2>.'s/:\(\w\+\)\s*=>\s*/\1: /g'

" FZF Configurations
if executable('fzf')
  let $FZF_DEFAULT_COMMAND = 'ag -g ""'

  " <C-p>to search files
  nnoremap <silent> <C-p> :FZF -m<cr>

  " <M-p> for open buffers
  nnoremap <silent> <M-p> :Buffers<cr>

  " Better search history
  command! QHist call fzf#vim#search_history({'right': '40'})
  nnoremap q/ :QHist<CR>

" Enable per-command history.
  " CTRL-N and CTRL-P will be automatically bound to next-history and
  " previous-history instead of down and up. If you don't like the change,
  " explicitly bind the keys to down and up in your $FZF_DEFAULT_OPTS.
  let g:fzf_history_dir = '~/.vim/share/fzf'

  " Customize fzf colors to match your color scheme
  let g:fzf_colors =
      \ { 'fg':      ['fg', 'Normal'],
      \ 'bg':      ['bg', 'Normal'],
      \ 'hl':      ['fg', 'Comment'],
      \ 'fg+':     ['fg', 'CursorLine', 'CursorColumn', 'Normal'],
      \ 'bg+':     ['bg', 'CursorLine', 'CursorColumn'],
      \ 'hl+':     ['fg', 'Statement'],
      \ 'info':    ['fg', 'PreProc'],
      \ 'border':  ['fg', 'Ignore'],
      \ 'prompt':  ['fg', 'Conditional'],
      \ 'pointer': ['fg', 'Exception'],
      \ 'marker':  ['fg', 'Keyword'],
      \ 'spinner': ['fg', 'Label'],
      \ 'header':  ['fg', 'Comment'] }
end

" NerdTree Configurations
nmap wm :NERDTree<cr>
let NERDTreeIgnore=['\.swp$']
silent! nmap <silent> <Leader>p :NERDTreeToggle<CR>
let g:NERDTreeWinSize = 30

" AG Configurations
if executable('ag')
  " Use Ag over Grep
  set grepprg=ag\ --nogroup\ --nocolor
endif

" bind K to grep word under cursor
nnoremap K :grep! "\b<C-R><C-W>\b"<CR>:cw<CR>
nnoremap \ :Ag<SPACE>

" ultisnips Configurations
let g:UltiSnipsExpandTrigger="<tab>"
let g:UltiSnipsJumpForwardTrigger="<c-b>"
let g:UltiSnipsJumpBackwardTrigger="<c-z>"

" lightline Configurations
set laststatus=2
set noshowmode
let g:lightline = {
    \ 'active': {
    \   'left': [['mode', 'paste'], ['readonly', 'relativepath', 'modified']]
    \ }}
