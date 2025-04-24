% M-file: mag_field.m
% Simulating the Rotating Magnetic Field in a 3-phase Stator

% Step 1: Set up basic conditions
bmax = 1;             % Normalized maximum magnetic field strength
freq = 60;            % Frequency in Hz
w = 2 * pi * freq;    % Angular velocity (rad/s)

% Step 2: Generate time vector for smooth animation
t = 0:1/6000:1/60;    % Time vector for one cycle (fine resolution)

% Step 3: Generate the three magnetic field components
Baa = sin(w * t) .* (cos(0) + 1i * sin(0));          % Phase A
Bbb = sin(w * t - 2*pi/3) .* (cos(2*pi/3) + 1i * sin(2*pi/3));  % Phase B
Bcc = sin(w * t + 2*pi/3) .* (cos(-2*pi/3) + 1i * sin(-2*pi/3)); % Phase C

% Step 4: Calculate the net magnetic field
Bnet = Baa + Bbb + Bcc;

% Step 5: Generate reference circle for visualization
circle = bmax * (cos(w * t) + 1i * sin(w * t));

% Step 6: Plotting the results
figure; % Create a figure window
for il = 1:length(t)
    clf;  % Clear the figure for the next frame
    
    % Plot the reference circle
    plot(real(circle), imag(circle), 'k--');  
    hold on;

    % Plot the individual magnetic fields
    plot([0 real(Baa(il))], [0 imag(Baa(il))], 'k', 'LineWidth', 2); % Phase A (Black)
    plot([0 real(Bbb(il))], [0 imag(Bbb(il))], 'b', 'LineWidth', 2); % Phase B (Blue)
    plot([0 real(Bcc(il))], [0 imag(Bcc(il))], 'm', 'LineWidth', 2); % Phase C (Magenta)

    % Plot the net magnetic field (Resultant)
    plot([0 real(Bnet(il))], [0 imag(Bnet(il))], 'r', 'LineWidth', 3); % Resultant (Red)

    % Axis settings
    axis square;
    axis([-1.5 1.5 -1.5 1.5]); % Adjusted for better visualization

    drawnow;
    hold off;
end