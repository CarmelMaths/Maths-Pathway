document.getElementById('mathStrength').addEventListener('input', function() {
    document.getElementById('mathStrengthValue').innerText = this.value;
});

function limitSelection(group, limit) {
    const checkboxes = document.querySelectorAll(`.${group}`);
    const checked = document.querySelectorAll(`.${group}:checked`);
    
    if (checked.length >= limit) {
        checkboxes.forEach((checkbox) => {
            if (!checkbox.checked) {
                checkbox.disabled = true;
            }
        });
    } else {
        checkboxes.forEach((checkbox) => {
            checkbox.disabled = false;
        });
    }
}

function determinePathway() {
    const interests = document.querySelectorAll('.interest:checked');
    const jobs = document.querySelectorAll('.job:checked');
    const mathStrength = document.getElementById('mathStrength').value;

    let interestScore = interests.length;
    let jobScore = jobs.length;

    let pathway = '';

    if (mathStrength >= 80 && interestScore >= 1 && jobScore >= 1) {
        pathway = 'Specialist/Methods';
    } else if (mathStrength >= 60 && interestScore >= 1 && jobScore >= 1) {
        pathway = 'Methods';
    } else if (mathStrength >= 40 && interestScore >= 1 && jobScore >= 1) {
        pathway = 'Applications';
    } else {
        pathway = 'General';
    }

    document.getElementById('recommendedPathway').innerText = `We recommend you follow the ${pathway} mathematics pathway.`;

    // Enable the reset button
    document.getElementById('resetButton').disabled = false;
}

function resetForm() {
    // Reset all checkboxes
    document.querySelectorAll('input[type="checkbox"]').forEach(checkbox => {
        checkbox.checked = false;
        checkbox.disabled = false;
    });

    // Reset the slider
    document.getElementById('mathStrength').value = 50;
    document.getElementById('mathStrengthValue').innerText = 50;

    // Clear the recommendation
    document.getElementById('recommendedPathway').innerText = 'Your pathway will be shown here.';

    // Disable the reset button
    document.getElementById('resetButton').disabled = true;
}
