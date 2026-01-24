# Sentiment Analysis on Comments - LaTeX Research Paper

Cấu trúc dự án LaTeX để viết bài nghiên cứu về phân tích cảm xúc bình luận.

## Cấu trúc thư mục

```
sentiment-analysis-comments/
├── main.tex              # File chính của tài liệu
├── packages.tex          # Các gói và cấu hình LaTeX
├── references.bib        # Danh mục tài liệu tham khảo
├── sections/             # Các phần của bài viết
│   ├── 01-introduction.tex
│   ├── 02-related-work.tex
│   ├── 03-methodology.tex
│   ├── 04-experiments.tex
│   └── 05-conclusion.tex
├── figures/              # Thư mục chứa hình ảnh
├── images/               # Thư mục chứa ảnh khác
└── tables/               # Thư mục chứa bảng
```

## Biên dịch (Compile)

### Sử dụng command line:

```bash
# XeLaTeX (khuyến nghị cho tiếng Việt)
xelatex main.tex
biber main
xelatex main.tex
xelatex main.tex

# Hoặc PDFLaTeX
pdflatex main.tex
biber main
pdflatex main.tex
pdflatex main.tex
```

### Sử dụng LaTeX editor (Overleaf, TeXShop, TeXworks):

1. Chọn `XeLaTeX` làm compiler
2. Build project

### Single command (Linux/Mac):

```bash
latexmk -xelatex main.tex
```

## Ghi chú

- Sử dụng `XeLaTeX` để hỗ trợ tiếng Việt tốt hơn
- Thêm hình ảnh vào thư mục `figures/` và tham chiếu trong LaTeX
- Thêm tài liệu tham khảo vào file `references.bib`
