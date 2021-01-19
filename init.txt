syntax enable


set t_Co=256   " This is may or may not needed."
set background=dark
colorscheme gruvbox

set encoding=utf-8

:set wrap!
:set nowrap
:set number relativenumber
:set nu rnu

set tabstop=4
set softtabstop=4
set shiftwidth=4

set splitbelow
set splitright

"split navigations
nnoremap <C-J> <C-W><C-J>
nnoremap <C-K> <C-W><C-K>
nnoremap <C-L> <C-W><C-L>
nnoremap <C-H> <C-W><C-H>
noremap <F8> :%y+<CR>

noremap <F6> :NERDTreeToggle<CR>

set textwidth=0 wrapmargin=0

call plug#begin()

Plug 'NLKNguyen/papercolor-theme'
Plug 'morhetz/gruvbox'

Plug 'neoclide/coc.nvim', { 'branch': 'release' }
Plug 'junegunn/fzf', {'do': { -> fzf#install() }}
Plug 'junegunn/fzf.vim'
Plug 'scrooloose/nerdtree', { 'on':  'NERDTreeToggle' }
Plug 'tpope/vim-fireplace', { 'for': 'clojure' }

Plug 'kien/ctrlp.vim'
Plug 'vim-airline/vim-airline'
Plug 'vim-airline/vim-airline-themes'

Plug 'jiangmiao/auto-pairs'

call plug#end()

nmap <leader>gd <Plug>(coc-definition)
nmap <leader>gr <Plug>(coc-references)
nnoremap <C-p> :GFiles<CR>

" use <tab> for trigger completion and navigate to the next complete item
function! s:check_back_space() abort
  let col = col('.') - 1
  return !col || getline('.')[col - 1]  =~ '\s'
endfunction

inoremap <silent><expr> <Tab>
  \ pumvisible() ? "\<C-n>" :
  \ <SID>check_back_space() ? "\<Tab>" :
  \ coc#refresh()

" use <c-space>for trigger completion
inoremap <silent><expr> <c-space> coc#refresh()

" use <c-space>for trigger completion
inoremap <silent><expr> <NUL> coc#refresh()

"Use <Tab> and <S-Tab> to navigate the completion list:
inoremap <expr> <Tab> pumvisible() ? "\<C-n>" : "\<Tab>"
inoremap <expr> <S-Tab> pumvisible() ? "\<C-p>" : "\<S-Tab>"

" custom tab for different programming languages 
au BufNewFile,BufRead *.py
    \  set tabstop=4
    \| set softtabstop=4
    \| set shiftwidth=4
    \| set textwidth=79
    \| set expandtab
    \| set autoindent
    \| set fileformat=unix
autocmd FileType python map <buffer> <F9> :w<CR>:exec '!python' shellescape(@%, 1)<CR>
autocmd FileType python imap <buffer> <F9> <esc>:w<CR>:exec '!python' shellescape(@%, 1)<CR>

au BufNewFile,BufRead *.cpp
    \  set tabstop=4
    \| set softtabstop=4
    \| set shiftwidth=4
	\| map <F9> :!g++ -g % -o %:r && ./%:r <CR>		

au BufNewFile,BufRead *.js, *.html, *.css
    \  set tabstop=2
    \| set softtabstop=2
    \| set shiftwidth=2

