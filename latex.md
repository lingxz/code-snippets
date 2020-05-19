# Latex

Include figure

```text
\begin{figure}
  \centering
  \includegraphics[height=0.5\linewidth]{images/filename.png}
  \caption{Some caption}
  \label{fig:some-figure}
\end{figure}
```

Using `hyperref` and the correct labels with `autoref` \(Eq. 1 instead of Equation 1 and Fig. 1 instead of Figure 1\)

```text
\usepackage[english]{babel}
\usepackage[%
  colorlinks = true,
  citecolor  = RoyalBlue,
  linkcolor  = RoyalBlue,
  urlcolor   = RoyalBlue,
  ]{hyperref}
  
\addto\extrasenglish{%
  \renewcommand{\chapterautorefname}{Chapter}%
  \renewcommand{\figureautorefname}{Fig.}%
  \renewcommand{\equationautorefname}{Eq.}%
  \renewcommand{\sectionautorefname}{Section}%
  \renewcommand{\subsectionautorefname}{Section}%
}
```

Continuous figure labeling in book class \(Fig 1, 2, 3 instead of Fig 1.1, 2.1, 2.2...\)

```text
\usepackage{chngcntr}
\counterwithout{figure}{chapter}
```

Subfigures side by side

```text
\begin{figure}
\centering
\subcaptionbox[Short Subcaption]{%
    $\Omega_{\Lambda} = 0\textup{---}0.99$%
    \label{subfig:sublabel1}%
}
[%
    0.5\textwidth % width of caption
]%
{%
    \includegraphics[width=0.5\textwidth]%
    {images/flat_const_rh.png}%
}%
% \hspace{0.1\textwidth} % seperation
\subcaptionbox[Short Subcaption]{%
    $\Omega_{\Lambda} = 0 \textup{---} 0.95$%
    \label{subfig:sublabel2}%
}
[%
    0.5\textwidth % width of caption
]%
{%
    \includegraphics[width=0.5\textwidth]%
    {images/flat_const_rh2.png}%
}%
\caption[Short Caption]{Results of the numerical simulation in flat space when $r_h$ is kept constant instead of $M$. The comoving size of the hole was fixed at $\SI{2.60}{\mega\parsec}$. This is the size such that at $\Omega_{\Lambda} = 0$, $M = 10^{13}M_{\odot}$. The left figure contains the full range from $\Omega_{\Lambda} = 0$ to 0.99, whereas the right figure is the slightly zoomed in version after removing two of the rightmost points, to make the differences at lower $\Omega_{\Lambda}$ more apparent.}
\label{fig:flat-const-rh}
\end{figure}
```

