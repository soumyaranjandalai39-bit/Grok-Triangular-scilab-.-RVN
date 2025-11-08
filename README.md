# Grok-Triangular-scilab-.-RVN
// Scilab code for Fourier series approximation of a triangular wave
// The triangular wave is even, periodic with period 2*pi, amplitude 1 (peaks at 1, troughs at -1)

// Clear workspace
clc;
clf;

// Parameters
N_terms = 20;  // Number of odd harmonics (k=0 to N_terms-1)
t = linspace(-2*%pi, 4*%pi, 2000);  // Time vector for multiple periods to visualize periodicity

// Compute Fourier series approximation
fs_approx = zeros(size(t));
for k = 0:N_terms-1
    n = 2*k + 1;  // Odd harmonics: 1,3,5,...
    a_n = 8 / (%pi^2 * n^2);
    fs_approx = fs_approx + a_n * cos(n * t);
end

// Define the original triangular wave function
function y = tri_wave(t)
    theta = modulo(t + %pi, 2*%pi) - %pi;  // Shift to [-pi, pi] interval
    y = 1 - (2 / %pi) * abs(theta);
endfunction

y_orig = tri_wave(t);

// Plot the results
subplot(2,1,1);
plot(t, y_orig, 'b-', 'LineWidth', 2);
title('Original Triangular Wave');
xlabel('t');
ylabel('f(t)');
xgrid(1);

// Plot the Fourier approximation
subplot(2,1,2);
plot(t, fs_approx, 'r-', 'LineWidth', 2);
title(sprintf('Fourier Series Approximation (N = %d terms)', N_terms));
xlabel('t');
ylabel('Approximation');
xgrid(1);
